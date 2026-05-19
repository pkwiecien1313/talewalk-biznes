# Plan działania — walidacja partnerów + wpływ na listę zadań

> **Cel:** w ciągu 4-6 tygodni zwalidować ścieżkę B (model prowizyjny od partnerów) z [`../strategy.md`](../strategy.md). Jeśli pozytywnie — zmieniamy kierunek. Jeśli nie — wracamy do A (model subskrypcyjny jak w obecnym kodzie).

Sporządzono: 2026-05-17.

---

## Plan 4 tygodnie

### Tydzień 1 — Przygotowanie + 3-5 pierwszych telefonów

**Cel:** zwalidować że problem partnerski jest realny.

> **Liczby — co oznaczają:** dzwonimy do **10-15 lokali** żeby zebrać dane do decyzji. Z tej grupy realnie podpisze list intencyjny **5-10 lokali** (to jest cel pierwszej fazy programu — patrz [`../strategy.md`](../strategy.md) sekcja Partner Program i [`../partner-program.md`](../partner-program.md) Phase 1). Część odmówi, część chce poczekać, część odpadnie po spotkaniu.

- [ ] Wybrać 10-15 partnerów docelowych z listy poniżej (z tego ~5-10 ma realnie podpisać)
- [ ] Zarezerwować 2 sesje telefonowania po 90 min (np. środa rano, piątek przed południem)
- [ ] Wykonać 3-5 telefonów w sesji 1 (środa)
- [ ] Wypełnić arkusz po każdej rozmowie (max 5 min po rozmowie)

**Co dalej** (decyzja na koniec tygodnia 1):
- 3+ pozytywnych ("byłoby zainteresowane, pokaż jak to działa") → kontynuujemy, tydzień 2 = pokaz aplikacji
- 1-2 pozytywne → kontynuujemy z innymi pytaniami (może problem z naszą obietnicą lub typami partnerów)
- 0 pozytywnych → wstrzymujemy zmianę kierunku, redefinicja modelu lub powrót do A

### Tydzień 2 — Wersja pokazowa aplikacji (1-2 dni) + kolejne 5 telefonów

**Cel:** mieć coś pokazywalnego, pogłębić walidację.

- [ ] Gałąź w kodzie `feat/partner-mock-demo`:
  - Karta miejsca: przykładowa odznaka "🎟 10% rabat — pokaż ekran przed zamówieniem" (przełącznik w panelu deweloperskim)
  - Nowy ekran: "Ekran rabatu" z kodem QR + nazwa lokalu + data ważności
  - Nowa strona `/dev/partner-dashboard` (przykładowy widok z perspektywy partnera): "Wizyty z Talewalk: 12 w tym tygodniu, prowizja 60zł", lista wizyt z dokładnym czasem
  - **Zero serwera** — wszystko statyczne, przykładowe dane jak reszta Etapu 1
- [ ] Kolejne 3-5 telefonów (czwartek/piątek)
- [ ] Po telefonach: zaplanować 2-3 wizyty osobiste w lokalach które wykazały zainteresowanie

### Tydzień 3 — Wizyty osobiste z pokazem + przygotowanie listu intencyjnego

**Cel:** od deklaracji do podpisanej intencji.

- [ ] Wydrukować jednostronicowy dokument (1 strona A4 z najważniejszymi informacjami) z opisem działania + główną obietnicą dla partnera + przykładowymi liczbami
- [ ] Przygotować wzór listu intencyjnego (list intencyjny — niewiążący prawnie dokument na 1 stronę: "rozważyłbym współpracę na warunkach X")
- [ ] 3-5 wizyt osobistych w lokalach (15-30 min każda)
- [ ] Po każdej wizycie: aktualizacja arkusza z notatkami, prośba o podpisanie listu intencyjnego w e-mailu kontrolnym (wysłanym po spotkaniu)

### Tydzień 4 — Punkt decyzyjny (zmiana kierunku lub powrót do A)

**Kryteria decyzji:**
- **5+ podpisanych listów intencyjnych lub silnych ustnych deklaracji** → **decyzja: idziemy w kierunku** ścieżki B/C. Reorganizacja listy zadań (patrz niżej), nowa duża inicjatywa "Program partnerski" w Jira
- **2-4 listy intencyjne** → wynik niejednoznaczny (część "tak", część "nie"). Możliwa hybrydowa ścieżka C (subskrypcja + prowizje). Rozważyć kolejny tydzień rozmów
- **Mniej niż 2 listy intencyjne** → wycofanie się do A. Wracamy do KAN-16 jak w planie, eksploracja zamknięta

---

## Lista celów (Bydgoszcz, centrum + Stare Miasto)

Mieszanka typów lokali — to ma znaczenie, bo różne typy inaczej płacą za przyprowadzonych klientów. Pierwsza piątka = priorytet (mała bariera wejścia, najbardziej prawdopodobny "tak").

### Restauracje + bary (Stary Rynek, Wełniany Rynek, ul. Długa, Mostowa)

- **Weranda Café** (Mostowa 5) — turystyczna, sprawdzą się pierwsi
- **Wodnik** (Stary Rynek) — duża restauracja, mają budżet marketingowy
- **Spichrze nad Brdą Bistro** (Grodzka) — w punkcie turystycznym, oczywiste partner
- **Restauracja Bistro Stary Rynek** (różne na rynku) — kilka opcji do testowania
- **Pierogarnia Stary Toruń / Mąka i Woda** (Długa) — niski średni rachunek, łatwa decyzja
- **Kawiarnia Familijna** (Stary Rynek) — kawiarnie zwykle łatwiej testować

### Kawiarnie + cukiernie

- **Cukiernia Sowa** (kilka lokalizacji) — sieć, ale siedziba w Bydgoszczy więc decyzja lokalna
- **Pijalnia Czekolady Wedel** (Stary Rynek) — turystyczna lokalizacja
- **Hej Café / Czachorowski** (Długa)

### Atrakcje + muzea

- **Muzeum Okręgowe** (Gdańska) — bilet 12-20 zł, łatwa prowizja
- **Exploseum** (Bydgoszcz) — turystyka specjalistyczna, idealni do testu w niszy
- **Wieża Ciśnień** (Filaretów) — punkt widokowy z biletem

### Sklepy z pamiątkami + miejscowymi produktami

- **Sklep "Bydgoszcz na półce"** (jeśli istnieje pod różnymi nazwami)
- **Galeria sztuki lokalnej** (Długa, Mostowa)

**Skąd brać numery:** Profil lokalu w Mapach Google (numer zwykle widoczny), strona internetowa, lokalne grupy Facebook ("Bydgoszcz restauracje").

**Kogo pominąć w pierwszej rundzie:**
- Sieciówki (McDonald's, KFC, Starbucks) — decyzja w centrali firmy, nie w lokalu
- Bary szybkiej obsługi / niskocenne (poniżej 20 zł średni rachunek) — prowizja 2 zł nie warta zachodu
- Hotele — to wymaga innego modelu (rozliczenia od rezerwacji, dłuższe negocjacje, większe kwoty)

---

## Wzór rozmowy (3-5 min)

> **Pamiętaj:** to rozmowa poznawcza, NIE sprzedażowa. Nie sprzedajesz. Pytasz. Im więcej oni mówią tym lepiej.

### Wstęp (15 s)

> "Dzień dobry, [imię]? Z tej strony Paweł Kwiecień. Buduję aplikację turystyczną dla Bydgoszczy i robię szybką ankietę z lokalami — kilka pytań w 3-4 minuty, czy ma pan/pani moment?"

Jeśli "teraz nie" → "Kiedy lepiej oddzwonić, w środę rano?"

### Trzy kluczowe pytania (2-3 min)

1. **Skąd przychodzą klienci?**
   > "Z jakich źródeł teraz przychodzą do was klienci? Ile procentowo to turyści, a ile mieszkańcy?"

   Cel: zrozumieć czy oni *mają* problem ze ściągnięciem turystów.

2. **Co już płacą za przyprowadzanie klientów?**
   > "Czy korzystacie z platform pobierających prowizję za klientów — Pyszne, Booking, TripAdvisor, reklamy Google? Jakie tam są prowizje i koszty?"

   Cel: ustalić punkt odniesienia cenowy i język rynkowy. Jeśli płacą 15-20% w Pyszne — 10% w Talewalk wygląda atrakcyjnie.

3. **Akceptowalność prowizji + sposób weryfikacji wizyty**
   > "Wyobraźcie sobie: aplikacja kieruje turystę do was, dostaje 10% rabatu pokazując ekran kelnerowi, my potem widzimy że wizyta się odbyła i pobieramy 10% prowizji od jego rachunku. Czy taki model w ogóle wam pasuje? Jaka prowizja byłaby do zaakceptowania, a jaka by was wyśmiała?"

### Pogłębienie — jeśli zainteresowani (1-2 min)

- "Co was zniechęca do podobnych ofert? Co was odrzuca w Pyszne / Bookingu?"
- "Czy uznawanie rabatu przez pokazanie ekranu z kodem QR jest technicznie wykonalne dla obsługi?"
- "Jakie minimum wizyt miesięcznie musiałoby przyjść, żeby warto było wam wejść?"

### Zamknięcie (15 s)

> "Super, dzięki. Jeśli pójdziemy dalej, czy mogę za 2 tygodnie odezwać się z pokazem jak to wygląda od strony użytkownika? Skontaktować się mailem czy telefonem?"

**KLUCZOWE:** notuj adres e-mail + preferowaną formę dalszego kontaktu.

---

## Arkusz — szablon notatek

Arkusz Google Sheets z kolumnami:

| Lokal | Typ | Osoba | Telefon | Data rozmowy | Ocena 1-5 | Skąd klienci | Płacą za przyprowadzanie? (gdzie/%) | Akceptowalna prowizja | Czy QR / ekran do weryfikacji OK? | Minimum wizyt/mies | Co zniechęca | Następny kontakt | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

**Ocena rozmowy 1-5:**
- 5 = "tak, ekscytujące, pokaż jak to działa"
- 4 = "ciekawe, pokaż jak to działa"
- 3 = "może, jeśli zadziała"
- 2 = "raczej nie, mam wątpliwości"
- 1 = "nie, mamy już wszystko czego nam trzeba"

**Próg do dalszych kroków:** średnia 3.5+ z 5-10 telefonów = zielone światło.

---

## Wpływ na listę zadań Etapu 1

Aktualny stan (duża inicjatywa KAN-4):

| Zadanie | Status | Wpływ zmiany kierunku B/C | Akcja |
|---|---|---|---|
| KAN-5 Setup projektu | ✅ Zrobione | brak | — |
| KAN-6 Przykładowe dane | ✅ Zrobione | brak | — |
| KAN-7 Logowanie (atrapa) | ✅ Zrobione | brak | — |
| KAN-8 Mapa | ✅ Zrobione | brak | — |
| KAN-11 Nawigacja — szkielet | ✅ Zrobione | brak | — |
| **KAN-13 Nawigacja — akcje** | 🔵 W toku | brak | **kończymy normalnie** — gałąź `feat/kan-13-navigation-actions` |
| KAN-9 Kreator planowania | ⚪ Do zrobienia | średni | wycofać limit modyfikacji wycieczki z kreatora |
| KAN-10 Edytor wycieczki | ⚪ Do zrobienia | średni | jw |
| KAN-12 Lista wycieczek | ⚪ Do zrobienia | niski | bez zmian, niezależne |
| KAN-14 Historia | ⚪ Do zrobienia | niski | bez zmian, niezależne |
| KAN-15 Profil + Ustawienia | ⚪ Do zrobienia | średni | wycofać sekcję subskrypcji, zostawić motyw / język / powiadomienia |
| **KAN-16 Paywall + Subskrypcje** | ⚪ Do zrobienia | **wysoki** | **WSTRZYMAĆ** do tygodnia 4 / punktu decyzyjnego |

### Co robić w tych 4 tygodniach walidacji

**Bezpieczne — kontynuować bez zmian:**
1. Dokończyć KAN-13 (w toku, mały zakres, niezależny od monetyzacji)
2. KAN-14 Historia — kolejny w kolejce, neutralny
3. KAN-12 Lista wycieczek — neutralny

**Wstrzymać:**
- KAN-16 całkowicie do punktu decyzyjnego

**Zmodyfikować jeśli zaczynane:**
- KAN-9/10 — w opisach zadania usunąć referencje do limitu modyfikacji wycieczki; trzymać limit w kodzie ale nie blokować przez interfejs
- KAN-15 — zostawić sekcję "Konto" + "Wygląd" + "Język" + "Powiadomienia"; sekcja "Subskrypcja" → przykładowa zaślepka "wkrótce"

### Nowe zadanie — Wersja pokazowa programu partnerskiego (tydzień 2)

Sugerowany format Jira:

**KAN-?? `[Talewalk][Partner — pokaz] Odznaka + ekran rabatu + panel partnera`**

Zakres:
- W `PlaceCard.vue` przykładowa odznaka "🎟 10% rabat" przy wybranych miejscach (lista zapisana na sztywno w przykładowych danych)
- Nowy ekran `DiscountScreen.vue` — kod QR + nazwa lokalu + data, dostępny przez przycisk w odznace
- Nowa strona `/dev/partner-dashboard` (dostępna TYLKO przez panel deweloperski) — przykładowa tabela wizyt + suma prowizji
- Przełącznik w panelu deweloperskim do włączania/wyłączania odznak

Etykieta: `partner-validation`, czas realizacji: 1-2 dni.

### Nowa duża inicjatywa (warunkowo po punkcie decyzyjnym)

**Jeśli punkt decyzyjny = zmiana kierunku zatwierdzona:**

Utworzyć inicjatywę `[Talewalk] Etap 1.5 — Program partnerski` z zadaniami:
- Panel administratora partnerów (pełna edycja + konfiguracja ofert + prowizja %)
- Warstwa atrybucji (generowanie kodów QR + weryfikacja wizyty)
- Konfiguracja modelu rozliczeń (Scenariusz A — patrz [`../partner-program.md`](../partner-program.md)): fakturowanie partnerów raz w miesiącu, bez Stripe Connect
- Panel przychodów dla partnera
- Funkcja serwerowa Firebase do weryfikacji wizyty

KAN-16 (Paywall) przenosi się do Etapu 6 i staje się opcjonalny (tylko dla zaawansowanych użytkowników).

### Etapy 2-7 — implikacje strategiczne

| Etap | Stan obecny | Wpływ zmiany kierunku B/C | Komentarz |
|---|---|---|---|
| 2. Firebase Auth + Firestore | Plan | brak | potrzebny zarówno użytkownikom jak partnerom |
| 3. Mapa Mapbox + Google Places | Plan | brak | podstawowa funkcja, niezmieniona |
| 4. Transport MZK | Plan | brak | podstawowa funkcja |
| 5. **AI + audio** (Claude + synteza mowy TTS) | Plan | **przyspieszyć** | to jest fosa konkurencyjna — przewaga trudna do skopiowania (patrz słowniczek w [`../strategy.md`](../strategy.md)); można zacząć już w Etapie 2 równolegle |
| 6. **Płatności** (Stripe + RevenueCat) | Plan | **zmiana kierunku** | w pierwszej wersji programu — bez Stripe Connect, rozliczenie przez fakturowanie partnerów raz w miesiącu (Scenariusz A w [`../partner-program.md`](../partner-program.md)). Stripe Connect (system Stripe do automatycznych wypłat dla partnerów) rozważać dopiero w fazie 2 lub 3, jako opcjonalne dodatkowe rozwiązanie. RevenueCat opcjonalny. |
| 7. Offline + PDF | Plan | niski | nadal funkcja Pro+, ale jeśli model prowizyjny — opcjonalny |

---

## Co przygotować zanim zaczniesz dzwonić

Konkretna lista do odhaczenia przed pierwszym telefonem:

- [ ] Lista 10-15 lokali z numerami (z Profili w Mapach Google → zwykle widoczne)
- [ ] Wzór rozmowy wydrukowany / otwarty na drugim ekranie
- [ ] Arkusz otwarty z gotowymi kolumnami
- [ ] Cisza w pokoju (zestaw słuchawkowy nieobowiązkowo)
- [ ] Notes papierowy obok — niektórym łatwiej notować ręcznie
- [ ] Przygotowane 2-3 zdania głównej obietnicy na wypadek pytania "po co to wszystko?":
  > "Buduję aplikację dla turystów odwiedzających Bydgoszcz — taki AI-przewodnik głosowy. Chcę zobaczyć czy lokale jak wasze mogą na tym też zarobić, więc zbieram opinie zanim coś zbuduję."

---

## Czego NIE robić w tych 4 tygodniach

- ❌ Nie podpisywać zobowiązań finansowych (rejestracja w Stripe Connect, biuro księgowe na program partnerski)
- ❌ Nie ogłaszać zmiany kierunku publicznie (LinkedIn, Facebook) — dopiero po punkcie decyzyjnym
- ❌ Nie wycofywać kodu subskrypcyjnego (`useSubscriptionStore`, `PLAN_LIMITS`) — może wrócimy do tego
- ❌ Nie modyfikować KAN-16 w Jira (zostaje w "Do zrobienia") — to oznaczenie statusu, nie zaczynamy jeszcze pracy
- ❌ Nie umawiać się z 10 partnerami jednocześnie — szykuj się maksymalnie 3-5 na sesję żeby było czasu na notatki + chwilę oddechu

---

## Pytanie kontrolne dla siebie po każdej rozmowie

Zapisz w arkuszu jednozdaniową odpowiedź:

> **Co ja się dziś dowiedziałem, czego nie wiedziałem rano?**

Jeśli 5 telefonów później odpowiedzi się powtarzają → wystarczy danych do decyzji.
Jeśli każda odpowiedź to nowy wniosek → masz fragmentaryczne rozumienie, potrzeba więcej rozmów (lub przebudowy pytań).
