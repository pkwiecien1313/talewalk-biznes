# Partner Program — wsparcie partnerów biznesowych (wersja techniczna)

> **Status:** dokument projektowy. Zakłada że pivot do ścieżki B/C został zatwierdzony (patrz [`strategy.md`](strategy.md)). Do tego czasu — referencja do dyskusji, brak implementacji w kodzie.
>
> **Powiązane wersje dokumentu:**
> - [`team-onboarding/partner-program-biznes.md`](team-onboarding/partner-program-biznes.md) — wersja bez żargonu, dla potencjalnego partnera (restauratora)
> - [`team-onboarding/partner-program-sprzedaz.md`](team-onboarding/partner-program-sprzedaz.md) — przewodnik dla sprzedawcy pozyskującego partnerów (wzory rozmów, gotowe odpowiedzi, cele tygodniowe)

Sporządzono: 2026-05-17. Ostatnia aktualizacja: 2026-05-19 (model rozliczeń A vs B, linki krzyżowe do wersji biznesowej i sprzedażowej).

---

## Vision — po co istnieje program

Aplikacja Talewalk kieruje turystów do lokalnych miejsc (restauracje, kawiarnie, atrakcje, sklepy z pamiątkami). Partner program zamienia tę "wartość kierowania" na realną wymianę gospodarczą:

- **Dla użytkownika:** zniżka na zamówienie / wejście / produkt (10-15% standard)
- **Dla partnera:** dodatkowy ruch klientów + prowizja-z-wartości (płacisz tylko za realne wizyty)
- **Dla Talewalk:** prowizja od atrybułowanych transakcji (10-15% od **ticket size** — wartości pojedynczego rachunku gościa w lokalu)

Model **win-win-win** — user nie płaci, partner płaci tylko za wynik, Talewalk skaluje z wykorzystaniem.

---

## Model rozliczeń — Scenariusz A vs Scenariusz B

To **fundamentalna decyzja architektoniczna** wpływająca na compliance (zgodność z prawem), stack techniczny i kto wystawia komu fakturę. W MVP wybieramy A, B traktujemy jako opcjonalny upgrade w Phase 2/3.

### Scenariusz A — User płaci tradycyjnie w lokalu (REKOMENDACJA MVP)

**Flow pieniędzy:**

```
Turysta ─── 100 zł (gotówka/terminal POS) ───▶ Partner
   ▲                                              │
   │                                              │ co miesiąc:
   │ rabat 8 zł zaaplikowany na rachunku          │ faktura 10 zł
   │ (kelner odlicza w lokalu)                    │ + VAT 23%
   │                                              ▼
   └──────────── Talewalk ◀──────────────────────┘
                (zapis wizyty, kalkulacja prowizji)
```

**Co się dzieje krok po kroku:**
1. Turysta pokazuje QR, kelner skanuje, wpisuje kwotę zamówienia (100 zł)
2. Turysta płaci kelnerowi normalnie (gotówka lub terminal POS) — **pieniądze nie przechodzą przez Talewalk**
3. Backend Talewalka zapisuje wizytę: `orderAmount: 100, commissionAmount: 10`
4. Na koniec miesiąca **Talewalk wystawia partnerowi fakturę** za prowizję
5. Partner przelewa kwotę faktury na konto firmowe Talewalk

**Kto fakturuje kogo:**
- **Talewalk → partner** (jedyna faktura w systemie)
- Typ usługi: *"Usługa marketingu afiliacyjnego — atrybuowane wizyty z aplikacji Talewalk"*
- Treść: *"Przykładowy miesiąc: 47 wizyt × średnio 8,50 zł prowizji = 399,50 zł netto + VAT 23% = 491,39 zł brutto"*
- Termin płatności: 14 dni
- Partner traktuje to jako koszt uzyskania przychodu (odliczy VAT)

**Plusy:**
- Nie potrzeba licencji MIP (Mała Instytucja Płatnicza — wpis do rejestru KNF, ~10-30k zł setup + compliance)
- Nie potrzeba Stripe Connect — wystarczy zwykły rachunek bankowy + księgowa
- Prosty model B2B znany każdej restauracji (jak Bilety24, Tripadvisor partnerzy, Google Ads)
- JDG (Jednoosobowa Działalność Gospodarcza) wystarczy — bez przekształcania na sp. z o.o.

**Minusy:**
- **Cash flow** (przepływ gotówki — kiedy pieniądze faktycznie wpadają na konto) opóźniony — Ty czekasz 14 dni na przelew od partnera
- Ryzyko nieopłaconych faktur (musisz windykować jak normalny dostawca usług)
- Partner może oszukać przy wpisywaniu kwoty zamówienia (zaniżyć żeby zmniejszyć prowizję) — mitigacja: random audits + user dispute

---

### Scenariusz B — User płaci za posiłek przez aplikację Talewalk (Phase 2+)

**Flow pieniędzy:**

```
Turysta ─── 100 zł (in-app payment Stripe) ───▶ Stripe Platform
                                                      │
                                          Stripe Connect rozdziela:
                                          ┌─────────┴─────────┐
                                          ▼                   ▼
                                       Talewalk            Partner
                                       (10 zł)             (90 zł)
```

**Co się dzieje:**
1. Turysta dostaje rachunek 100 zł — płaci kartą **w apce Talewalk** (nie u kelnera)
2. Stripe Connect rozdziela płatność: 10 zł zostaje u Talewalka, 90 zł trafia do partnera (na jego konto Stripe Connect Express)
3. Partner widzi w panelu *"Wypłata 90 zł za zamówienie #1234"*

**Kto fakturuje kogo (dwa wariant):**

*Wariant B1 — Talewalk jako platforma:*
- **Partner → turysta** (partner fakturuje gościa za 100 zł brutto — to *on* sprzedaje jedzenie, Talewalk tylko pośredniczy)
- **Talewalk → partner** (Ty wciąż fakturujesz partnera za prowizję 10 zł — jak w scenariuszu A)
- Stripe Connect technicznie ułatwia transfer, ale to nie zmienia kto komu sprzedaje usługę

*Wariant B2 — Talewalk jako "merchant of record" (sprzedawca formalny):*
- **Talewalk → turysta** (Ty fakturujesz gościa za 100 zł — Talewalk występuje jako sprzedawca platformowy)
- **Partner → Talewalk** (partner fakturuje Ciebie za 90 zł — Ty jesteś jego klientem)
- **WYMAGA statusu MIP albo agenta rozliczeniowego** (KNF compliance) — to deal-breaker dla MVP

**Plusy:**
- Natychmiastowy cash flow (pieniądze trafiają od razu do Talewalk + partner)
- Brak ryzyka nieopłaconych faktur (rozliczenie automatyczne)
- Możliwość in-app booking + płatność (lepszy UX dla turysty)

**Minusy:**
- Wymaga Stripe Connect (koszt: 0.25% + setup integracji)
- W wariancie B2 — wymaga MIP/agenta rozliczeniowego (deal-breaker dla JDG)
- Partner musi zintegrować Talewalk z kasą fiskalną (bo dostaje 90 zł zamiast 100 zł — trzeba uzgodnić jak rejestruje sprzedaż)
- Adopcja przez partnerów trudniejsza (musi zmienić proces obsługi)

---

### Decyzja: MVP = Scenariusz A

| Aspekt | A (tradycyjnie) | B (in-app payment) |
|---|---|---|
| Kompleksowość | niska | wysoka |
| Licencja MIP wymagana | nie | tak (wariant B2) |
| Stripe Connect | nie | tak |
| Cash flow | Ty czekasz 14 dni | natychmiast |
| Ryzyko nieopłaconych faktur | tak | nie |
| UX turysty | "płać u kelnera jak zwykle" | "zapłać w apce" |
| Adopcja partnerów | łatwa | trudna |
| Forma prawna Talewalk | JDG OK | JDG OK (B1) / wymaga sp. z o.o.+MIP (B2) |

**MVP (Phase 1):** Scenariusz A. **Phase 2/3:** opcjonalny upgrade do B1, gdy mamy 30+ partnerów i ryzyko nieopłaconych faktur urasta. **B2 tylko jeśli przekształcamy na sp. z o.o. + uzyskamy MIP.**

---

## User flows (strona aplikacji)

### Flow U1 — Discovery (znajdowanie partnerów)

```
User otwiera mapę / search
  ↓
POI z aktywną ofertą partnerską widoczne z badge "🎟 10%"
(np. kolorowa pinezka + ikona kuponu)
  ↓
Klika POI → karta miejsca z dodatkową sekcją:
  ┌─────────────────────────────────────┐
  │ 🎟 OFERTA SPECJALNA                 │
  │                                     │
  │ 10% rabat na całe zamówienie        │
  │ Ważne dziś, 12:00 - 22:00           │
  │                                     │
  │ [Aktywuj rabat]                     │
  └─────────────────────────────────────┘
```

**Detale UX:**
- Badge w PlaceCard tylko gdy oferta aktywna w danym dniu/godzinie
- W liście wyszukiwania osobne oznaczenie miejsc z ofertami
- Filtr w mapie: "Pokaż tylko miejsca z rabatami"
- Jeśli user dodaje partnera do wycieczki → bonus info: "Po wizycie wyślemy ci kod rabatowy"

### Flow U2 — Redemption (uzysk rabatu)

```
User klika [Aktywuj rabat]
  ↓
Sprawdzenia:
  - czy user jest fizycznie w lokalu (GPS ≤ 50m)?
    NIE → "Musisz być w lokalu żeby aktywować"
  - czy oferta dziś aktywna?
  - czy user nie wykorzystał już dzisiejszej oferty u tego partnera?
  ↓
Backend generuje unikalny visitId + QR code (TTL 15 min)
  ↓
Wyświetla screen:
  ┌─────────────────────────────────────┐
  │ Pokaż kelnerowi/kasjerowi:          │
  │                                     │
  │     ▓▓▓▓▓▓▓▓▓▓▓▓▓                  │
  │     ▓ QR CODE ▓                     │
  │     ▓▓▓▓▓▓▓▓▓▓▓▓▓                  │
  │                                     │
  │ Kod: A7K-9MX                        │
  │ Ważny do: 13:47                     │
  │ Rabat: 10% (max 30 zł)              │
  │                                     │
  │ [Zamknij]                           │
  └─────────────────────────────────────┘
  ↓
Kelner skanuje QR przez aplikację partnera
  → otwiera formularz "Wartość zamówienia"
  → wpisuje np. 80 zł
  → potwierdza
  ↓
Backend:
  - oblicza rabat = min(80 × 10%, 30) = 8 zł
  - oblicza prowizję Talewalk = 80 × 10% = 8 zł (od wartości brutto)
  - zapisuje visit jako 'redeemed'
  ↓
Aplikacja użytkownika dostaje push notification:
  "✅ Otrzymałeś 8 zł rabatu w [nazwa lokalu]"
  ↓
Po 30-60 min: opcjonalny prompt "Jak było? Oceń lokal"
```

**Edge cases U2:**
- **User nie jest w lokalu** — blokada generowania QR (anti-fraud)
- **Lokal nie zeskanował** — po 15 min QR wygasa, brak rabatu, brak prowizji
- **User pokazał screenshot QR** — QR jest jednorazowy + TTL, server-side validation
- **Order canceled przez partnera** — partner w panelu oznacza visit jako "refunded", korekta prowizji

### Flow U3 — Postać rabatu w pamięci wycieczki

```
Po zakończonej wizycie / wycieczce:
  ↓
W SCR-HIST-02 (szczegóły wycieczki):
  - lista visited places z odznakami "Aktywowano rabat: 8 zł"
  - sekcja "Twoje oszczędności podczas tej wycieczki: 25 zł"
  ↓
W SCR-AUTH-05 (profil):
  - łączna kwota zaoszczędzonych pieniędzy ever
  - kupon "1000 zł zaoszczędzone = darmowy miesiąc Pro" (ścieżka C hybrid)
```

---

## Partner flows (strona partnera)

### Flow P1 — Onboarding (rejestracja partnera)

```
Phase A (MVP — manual, ~30-50 partnerów):
  ↓
Talewalk sales rep odwiedza lokal:
  - prezentuje **value prop** (value proposition — propozycję wartości: jedno-zdaniowe wyjaśnienie korzyści dla partnera: "10% prowizji od atrybułowanych wizyt, brak opłat stałych, możliwość rezygnacji w każdej chwili — **opt-out anytime**")
  - podpisanie ramowej umowy partnerskiej (**LOI** czyli Letter of Intent — list intencyjny, niewiążący prawnie → po 1 miesiącu → **standard contract**, czyli właściwa umowa)
  ↓
Talewalk admin tool:
  - zakłada rekord partner w Firestore (nazwa, NIP, adres, kontakt)
  - linkuje do POI w mapStore (placeId)
  - konfiguruje ofertę: type, value, ważność (manual)
  ↓
Partner dostaje:
  - email z linkiem do panelu (web)
  - QR scanner app (PWA / Capacitor link)
  - naklejka na drzwi "🎟 Akceptujemy Talewalk — 10% rabat dla turystów"
  - krótki onboarding video (2 min)

Phase B (Scale — self-service, 50+ partnerów):
  ↓
Partner sam wchodzi na partners.talewalk.com / scan QR z plakatu
  ↓
Self-onboarding wizard:
  - dane firmy (NIP automatyczny lookup z GUS)
  - wybór POI z mapy (auto-suggest na podstawie adresu)
  - typ działalności (restauracja / kawiarnia / atrakcja / sklep)
  - propozycja oferty (default 10%, max 50 zł)
  - akceptacja regulaminu
  ↓
Stripe Connect onboarding (KYC):
  - dane do KYC (dowód, dane bankowe)
  - 1-3 dni na akceptację
  ↓
Po akceptacji → partner aktywny, oferta dostępna w aplikacji
```

### Flow P2 — Operacje codzienne (skanowanie QR + obsługa wizyty)

```
Personel obsługujący (kelner / kasjer / recepcja):
  ↓
Otwiera Partner Scanner App (web PWA na tablecie kasowym lub Capacitor app)
  ↓
Loguje się raz na zmianę (PIN code)
  ↓
Klient pokazuje QR z aplikacji Talewalk
  ↓
Personel skanuje (kamera tabletu / smartphone)
  ↓
Otwiera się ekran:
  ┌─────────────────────────────────────┐
  │ Klient z aplikacji Talewalk         │
  │                                     │
  │ Imię: Paweł K.                      │
  │ Rabat: 10% (max 30 zł)              │
  │                                     │
  │ Wartość zamówienia: [____] zł       │
  │                                     │
  │ Po rabacie: — zł                    │
  │                                     │
  │ [Anuluj]      [Potwierdź wizytę]    │
  └─────────────────────────────────────┘
  ↓
Wpisuje kwotę → live calc rabatu
  ↓
[Potwierdź] → backend rejestruje visit:
  - klient widzi push: "Otrzymałeś rabat 8 zł"
  - partner widzi: "Wizyta #245 zarejestrowana, prowizja Talewalk: 8 zł"
  ↓
Kelner kontynuuje obsługę normalnie (rabat zaaplikowany na rachunku)
```

**Wariant offline / brak skanera:**
- Personel wpisuje kod alfanumeryczny ręcznie (np. "A7K-9MX")
- Wymaga online weryfikacji (lokal musi mieć WiFi/4G)
- Fallback: tryb "trust mode" gdzie partner deklaruje wartość później (z dispute risk)

### Flow P3 — Dashboard + payouts (panel zarządczy partnera + wypłaty)

```
Partner Panel (web):
  ↓
Strona główna:
  - "Wizyty dzisiaj: 12 / W tym tygodniu: 67 / W tym miesiącu: 245"
  - "Łączna wartość atrybułowanych zamówień: 12 450 zł"
  - "Prowizja Talewalk (do zapłaty): 1 245 zł"
  - "Twoje przychody netto: 11 205 zł"
  - Lista ostatnich 20 wizyt (data, kwota, prowizja)
  ↓
Tab "Oferta":
  - Edycja typu/wartości rabatu
  - Godziny ważności (pause na lunch peak?)
  - Limit dziennych wizyt (np. "max 20" gdy lokal pęka w szwach)
  - Auto-pause przy reached limit
  ↓
Tab "Wypłaty":
  - Historia transferów
  - Następna wypłata: data + szacowana kwota
  - Stripe Connect status (KYC OK / wymaga update)
  - Konto bankowe (zmienić)
  ↓
Tab "Klienci":
  - Liczba unique users
  - Top 10 powracających
  - Ratings + feedback (opcjonalny od user)
  ↓
Tab "Spory":
  - Pending disputes (jeśli user kwestionuje że nie był)
  - Możliwość "approve" / "reject" w 48h, inaczej auto-resolve
```

**Rozliczenia (model docelowy zależny od Scenariusza A vs B):**

*Scenariusz A (MVP):* Talewalk fakturuje partnerów raz w miesiącu za prowizję od atrybułowanych wizyt. Partner przelewa kwotę faktury na rachunek firmowy Talewalk (termin 14 dni). Brak Stripe Connect — wystarczy zwykły przelew SEPA/Express Elixir.

*Scenariusz B1 (Phase 2 **opt-in** — partner sam wybiera czy chce ten model, domyślnie wyłączony):* Stripe Connect Express account (konto Express w Stripe Connect — uproszczony typ konta z minimalnym KYC) dla partnera. User płaci w apce, Stripe rozdziela 90/10. Cykl wypłat tygodniowy (Czwartek dla wizyt Mon-Sun poprzedniego tygodnia). **Threshold** (próg) minimum 50 zł — poniżej tej kwoty wypłata zostaje do następnego cyklu (żeby uniknąć drogich małych transferów).

*Scenariusz B2 (Phase 3, wymaga sp. z o.o. + MIP):* Talewalk jako "merchant of record" — kompleksowe rozliczenia z VAT.

---

## Data model (Firestore)

```typescript
// partners/{partnerId}
interface Partner {
  partnerId: string
  placeId: string                  // link do POI w mapStore
  name: string
  ownerName: string
  ownerEmail: string
  ownerPhone: string
  nip: string
  address: string
  bankAccount: string              // encrypted
  stripeAccountId: string | null   // Stripe Connect ID
  stripeKycStatus: 'pending' | 'active' | 'rejected'
  status: 'onboarding' | 'active' | 'paused' | 'terminated'
  commissionRate: number           // 0.10 = 10%
  createdAt: Timestamp
  activatedAt: Timestamp | null
}

// offers/{offerId} (subcollection partners/{partnerId}/offers)
interface Offer {
  offerId: string
  partnerId: string
  type: 'percentage' | 'fixed'
  value: number                    // 10 (=10%) lub 500 (=5zł w groszach)
  maxDiscountAmount: number        // max 30 zł = 3000 gr
  validFrom: Timestamp             // np. dziś
  validTo: Timestamp | null        // ongoing
  validDays: ('mon'|'tue'|...|'sun')[]
  validHoursFrom: string           // "12:00"
  validHoursTo: string             // "22:00"
  dailyVisitLimit: number | null   // null = unlimited
  active: boolean
}

// visits/{visitId}
interface Visit {
  visitId: string
  userId: string                   // Firebase Auth UID
  partnerId: string
  offerId: string
  qrCode: string                   // 8-char unique, np. "A7K9MXBR"
  generatedAt: Timestamp           // moment kliknięcia "Aktywuj"
  generatedAtCoords: GeoPoint      // GPS w momencie generacji (anti-fraud)
  redeemedAt: Timestamp | null     // moment skanu przez partnera
  expiredAt: Timestamp             // generatedAt + 15 min
  orderAmount: number | null       // wpisane przez partnera, w groszach
  discountAmount: number | null    // obliczone w groszach
  commissionAmount: number | null  // obliczone w groszach
  status: 'generated' | 'redeemed' | 'expired' | 'disputed' | 'refunded'
  disputeReason: string | null
  refundedAt: Timestamp | null
}

// payouts/{payoutId}
interface Payout {
  payoutId: string
  partnerId: string
  periodFrom: Timestamp
  periodTo: Timestamp
  visitCount: number
  totalOrderAmount: number         // suma wartości zamówień
  totalCommissionAmount: number    // suma prowizji
  stripeFee: number
  netAmount: number                // do wypłaty partnerowi
  stripeTransferId: string | null
  status: 'pending' | 'transferred' | 'failed'
  createdAt: Timestamp
  transferredAt: Timestamp | null
}

// disputes/{disputeId}
interface Dispute {
  disputeId: string
  visitId: string
  raisedBy: 'user' | 'partner'
  reason: string
  evidence: { url: string, type: 'photo' | 'gps_log' }[]
  status: 'open' | 'approved' | 'rejected'
  resolvedAt: Timestamp | null
  resolvedBy: string               // talewalk admin UID
}
```

---

## Architektura techniczna

```
┌─────────────────────────────────────────────────────────────────┐
│ USER APP (Ionic Vue)                                            │
│  - Discovery: badge na POI z aktywną ofertą                     │
│  - Redemption: generowanie QR + wyświetlenie                    │
│  - GPS validation: ≤ 50m od POI                                 │
│  - Push notifications (FCM): "Otrzymałeś X zł rabatu"           │
└─────────────────────────────────────────────────────────────────┘
              ↓ HTTPS                              ↑ FCM
┌─────────────────────────────────────────────────────────────────┐
│ FIREBASE FUNCTIONS (Node.js)                                    │
│  - generateQR(userId, partnerId, offerId, gps): visitId         │
│  - redeemQR(qrCode, orderAmount, partnerStaffId): result        │
│  - calculateCommission(orderAmount, commissionRate): amount     │
│  - createPayout(partnerId, period): payout                      │
│  - disputeRaise(visitId, reason): dispute                       │
└─────────────────────────────────────────────────────────────────┘
       ↓                    ↓                          ↓
┌──────────────┐  ┌─────────────────────┐  ┌─────────────────────┐
│ FIRESTORE    │  │ STRIPE CONNECT      │  │ FCM                 │
│ partners/    │  │ (tylko Scenariusz B │  │ - User push         │
│ offers/      │  │  — Phase 2+)        │  │ - Partner alerts    │
│ visits/      │  │ - KYC partnerów     │  │                     │
│ payouts/     │  │ - Transfers payouts │  │                     │
│ disputes/    │  │ - Refunds           │  │                     │
└──────────────┘  └─────────────────────┘  └─────────────────────┘
                  (w MVP — Scenariusz A:
                   faktury B2B + przelewy
                   tradycyjne, bez Stripe)
              ↑ HTTPS
┌─────────────────────────────────────────────────────────────────┐
│ PARTNER PANEL (web — Vue 3 / Nuxt, deploy Firebase Hosting)     │
│  - Auth: Firebase Auth (email + Google)                         │
│  - Dashboard: visits / earnings / payouts                       │
│  - Offer config: CRUD na offers                                 │
│  - QR Scanner: kamera z @capacitor-community/barcode-scanner    │
│                  lub MediaDevices API (web)                     │
│  - KYC: redirect do Stripe Connect onboarding                   │
└─────────────────────────────────────────────────────────────────┘
              ↓ admin operations
┌─────────────────────────────────────────────────────────────────┐
│ TALEWALK ADMIN PANEL (internal, separate auth)                  │
│  - Approve partners (manual w MVP)                              │
│  - Manage disputes                                              │
│  - Trigger payouts (manual w MVP)                               │
│  - Analytics + revenue reports                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Stack komponentów:**

| Komponent | Technologia | Hosting |
|---|---|---|
| User app | Ionic Vue 3 (istniejący) | App Store / Google Play / web |
| Partner panel | Vue 3 / Nuxt 3, web responsive | Firebase Hosting (`partners.talewalk.com`) |
| Partner scanner | PWA wbudowany w Partner panel | (jak wyżej) |
| Talewalk admin | Vue 3 / Nuxt, separate | Firebase Hosting (`admin.talewalk.com`, IP whitelist) |
| Backend | Firebase Functions Node.js | Firebase |
| Database | Firestore (multi-tenant) | Firebase |
| Auth | Firebase Auth | Firebase |
| Payments | Stripe Connect (Express accounts) | Stripe |
| Notifications | FCM | Firebase |
| QR generation | `qrcode` npm (client-side) | — |

---

## Security + anti-fraud

**Kluczowe wektory ataku + mitigacje:**

1. **User generuje QR, screenshot, później "redeems" gdy nie był**
   - GPS check przed generacją (≤ 50m od POI)
   - QR TTL 15 min (po wygaśnięciu invalid)
   - One-time use (server marks redeemed)
   - Partner musi fizycznie zeskanować z aplikacji partnera (nie da się "wpisać kodu" bez aplikacji)

2. **Partner fałszywie redeems QR żeby nabić prowizję sobie**
   - Wait, partner PŁACI prowizję, nie dostaje, więc nie ma motivu
   - Risk inversion: partner mógłby NIE redeem żeby uniknąć prowizji. Mitigation: user widzi w aplikacji "rabat zaaplikowany" — może dispute jeśli nie ma push w 10 min

3. **Partner zaniża orderAmount żeby zmniejszyć prowizję**
   - Random audits przez Talewalk team (sprawdzić paragony dla próbki)
   - User może dispute: "zapłaciłem X, partner wpisał Y"
   - Rating/feedback mechanism — partnerzy z dużym dispute rate są terminated

4. **Bot / fake users masowo generują QR**
   - Rate limit per user (max 5 redemptions / dzień)
   - **reCAPTCHA** (usługa Google weryfikująca że user jest człowiekiem, nie botem) na generację QR (opt-in — dla podejrzanych userów)
   - Phone verification dla nowych userów

5. **Personel partnera kradnie QR z innych klientów**
   - QR jest bezwartościowe bez konkretnej wizyty (single use, tied to user)
   - Partner staff loguje się PIN-em — audyt kto skanował

6. **Refund attack** (user kupuje za 1000 zł, partner wypłaca rabat 100 zł, user refunduje → 0 zł zamówienia, partner stratny 100 zł)
   - Partner w panelu może oznaczyć visit jako "refunded" w 48h
   - Korekta prowizji + zwrot rabatu
   - User reputation: dużo refundów = ban

---

## Phased rollout

### Phase 1 — MVP manual (3 mies, 5-10 partnerów)

**Goal:** walidacja modelu w terenie + fine-tune UX z prawdziwymi userami.

**Model rozliczeń:** Scenariusz A (user płaci tradycyjnie w lokalu, Talewalk fakturuje partnerów raz w miesiącu — patrz sekcja "Model rozliczeń").

**Scope:**
- Hardcoded partners + offers w Firestore (admin tool)
- Brak partner panel — operacje przez Talewalk staff (telefon/email)
- **Brak Stripe Connect** — rozliczenie przez faktury B2B Talewalk → partner, partner przelewa zwykłym przelewem na rachunek firmowy
- QR generation w app + bardzo prosty endpoint redeem (POST)
- Push notification po redeem
- Talewalk team manually handles disputes (rzadkie na tej skali)
- Comiesięczne fakturowanie partnerów (manual proces w księgowości, np. wFirma / iFirma / Comarch ERP)

**Effort:** ~3-4 tyg dev + sales partnership (osobny czas).

### Phase 2 — Beta (6-9 mies, 30-50 partnerów)

**Goal:** skalowanie operacji, automatyzacja.

**Model rozliczeń:** wciąż A (Talewalk fakturuje partnerów), ale automatyzujemy fakturowanie — backend Firebase Function generuje faktury PDF w cyklu miesięcznym, podpinając się przez API do oprogramowania księgowego (np. iFirma API). Stripe Connect rozważamy gdy >50 partnerów i ryzyko nieopłaconych faktur rośnie.

**Scope:**
- Partner panel (web) z **self-service** (samoobsługa — partner sam wykonuje czynności bez kontaktu z Talewalk staff):
  - **Onboarding wizard** (kreator rejestracji partnera — kilka kroków: dane firmy → wybór POI → ustawienie oferty → akceptacja regulaminu) + KYC (Know Your Customer — weryfikacja tożsamości właściciela firmy)
  - Offer CRUD (Create/Read/Update/Delete — pełna edycja ofert: dodawanie, podgląd, edycja, usuwanie)
  - Dashboard z visits + earnings
- QR Scanner PWA (Progressive Web App — aplikacja webowa działająca jak natywna)
- Automated invoicing — comiesięczna faktura PDF generowana z danych Firestore, email do partnera
- Disputes system (basic, admin reviewable)
- Notifications dla partnerów (nowa wizyta, payout, dispute)
- **Opcjonalnie:** Stripe Connect onboarding dla partnerów którzy preferują automatyczne rozliczenie (upgrade do B1 jako opt-in)

**Effort:** ~2-3 mies dev (zatrudnić juniora?), Stripe Connect compliance.

### Phase 3 — Scale (12+ mies, 100+ partnerów, multi-city)

**Goal:** skalowanie multi-city + integracje + zaawansowane features.

**Scope:**
- Integracje POS (Bookwise, iPOS) — auto-deduct rabatu bez ręcznego wpisywania
- Loyalty program (return customers bonus)
- A/B testing offerów
- Self-onboarding bez sales touch (lokal sam zarejestruje przez plakat QR)
- Multi-city support (oferty filtered per ACTIVE_CITY)
- API public dla partner integracji
- Talewalk-jako-marketplace ranking (top performers boost in app)

---

## Otwarte pytania biznesowe

Te wymagają decyzji przed startem implementacji:

1. **Standardowa prowizja** — 10%? 12%? 15%? Sprawdzić w discovery calls czy partnerzy akceptują (per `team-onboarding/action-plan-validation.md`)

2. **Minimum payout** (próg minimalnej wypłaty) — 50 zł, 100 zł, 200 zł? Im wyższy tym mniej **Stripe fees** (opłaty pobierane przez Stripe za każdy transfer, ~1-2 zł), ale partnerzy z małym ruchem czekają długo

3. **Cycle wypłat** — tygodniowy, miesięczny, **daily** (codzienny)? Tygodniowy = standard SaaS (modelu abonamentowego), ale wyższe Stripe transfer fees

4. **Maximum discount per visit** — czy partner ustawia (np. max 30 zł żeby nie spalić marży na drogie zamówienia)? Default policy

5. **Komu należy się rabat przy grupie** — każdy user osobno generuje QR? Jeden user = cała grupa? Jeden user × max kwota per grupa?

6. **Refund policy** — czy partner może refundować visit w 24h, 48h, 72h? Co jeśli user już dostał push o rabacie?

7. **Dispute resolution** — kto rozstrzyga? Manual przez Talewalk staff w MVP, później auto-rules + escalation?

8. **Exclusivity** — czy partner może być w Talewalk + Pyszne + Bookingu jednocześnie? Domyślnie tak (non-exclusive lepiej na start)

9. **Termination** — kto może rozwiązać współpracę i kiedy? 30-day notice obie strony? Immediate dla obvious fraud?

10. ~~**VAT i podatki**~~ — **ROZSTRZYGNIĘTE w sekcji "Model rozliczeń"**: w MVP Talewalk fakturuje partnerów (usługa marketingu afiliacyjnego), Scenariusz A. Pozostała otwarta kwestia: czy stosować VAT MP (mały podatnik) czy standardową stawkę 23% — do uzgodnienia z księgową przed wystawieniem pierwszej faktury.

---

## Otwarte pytania techniczne

1. **GPS validation accuracy** — w gęstej miejskiej zabudowie GPS może być ±20-50m. Tolerancja generacji QR — 50m czy 100m?

2. **Offline scanning** — co jeśli lokal nie ma WiFi w momencie skanu? Cache QR na app side z pending sync?

3. **QR format** — własny format alfanumeryczny czy standardowy URI (`talewalk://visit/A7K9MX`)? URI pozwala scan z jakimkolwiek QR readerem, ale podatne na social engineering ("zeskanuj ten QR i przyznaj rabat")

4. **Partner Scanner — natywna app czy PWA?** PWA prostsze deploy, natywna lepszy access do kamery. Capacitor wrap najprawdopodobniej

5. **Multi-staff support** — jak loguje się kilku kelnerów na jednym tablecie? PIN per osoba, shift switcher

6. **Real-time vs batch** — wizyty real-time do dashboardu (Firestore realtime) czy batch co minutę (less expensive)?

7. **Audit log** — Firestore native sufficient czy potrzebujemy BigQuery dla compliance + analytics?

---

## Co dalej

Po zatwierdzeniu **pivot** (zwrotu strategicznego) — **decision gate** (punkt decyzyjny opisany w `strategy.md`):

1. **Utworzyć epik Jira `[Talewalk] Etap 1.5 — Partner Program`**
2. **Sub-tickety dla Phase 1 MVP:**
   - Partner data model + Firestore rules
   - QR generation + redeem endpoint
   - User app: badge w PlaceCard + redemption screen
   - Push notification po redeem
   - Talewalk admin tool (manual partner CRUD)
3. **Sales:** sign 5-10 partnerów (Phase 1) — patrz `team-onboarding/action-plan-validation.md`
4. **Compliance:** rozmowa z księgową o:
   - VAT model dla faktur Talewalk → partner (stawka 23% vs zwolnienie MP)
   - Czy JDG (Jednoosobowa Działalność Gospodarcza) Webplanet wystarczy na MVP (Scenariusz A) — TAK
   - Stripe Connect i ew. licencja MIP (Mała Instytucja Płatnicza) — dopiero w Phase 2/3 przy upgrade do B
5. **Decyzja A/B testów** prowizji 10% vs 12% vs 15% — który najbardziej akceptowalny przez partnerów (sprawdzić w calls)
