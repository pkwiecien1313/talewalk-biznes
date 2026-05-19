# Talewalk dla partnerów biznesowych — jak to działa?

> Dokument dla restauratorów, właścicieli kawiarni, kierowników atrakcji turystycznych — wszystkich którzy rozważają dołączenie do programu partnerskiego Talewalk.
>
> Czas czytania: ~10 minut. Bez żargonu technicznego. Konkretne liczby i przykłady.
>
> **Powiązane dokumenty wewnętrzne (nie dla partnera):**
> - [`../partner-program.md`](../partner-program.md) — wersja techniczna (architektura, kod, integracje)
> - [`partner-program-sprzedaz.md`](partner-program-sprzedaz.md) — przewodnik dla sprzedawcy Talewalk

Sporządzono: 2026-05-19

---

## W jednym zdaniu

**Talewalk to aplikacja dla turystów odwiedzających Bydgoszcz, która kieruje ich do Twojego lokalu w zamian za 10% prowizji od rachunku — płacisz tylko za realnych klientów, których my przyprowadziliśmy.**

---

## Jak Twój gość trafia do Ciebie?

### Krok 1 — Turysta planuje spacer po Bydgoszczy

Turysta otwiera Talewalk. Aplikacja pokazuje mu mapę miasta z atrakcjami, restauracjami, kawiarniami, muzeami. Pomaga zaplanować trasę — np. "spacer Stary Rynek → Wyspa Młyńska → Brda" na 3 godziny z 5 przystankami.

### Krok 2 — Widzi Twoją ofertę

Twoja restauracja pokazuje się na mapie z **małym kuponem 🎟 10% rabat**. Turysta klika i widzi:

```
🎟 OFERTA SPECJALNA u "Weranda Café"
10% rabat na całe zamówienie
Ważne dziś, 12:00 - 22:00

[Aktywuj rabat]
```

### Krok 3 — Przychodzi do Ciebie

Turysta klika "Aktywuj rabat" **tylko gdy fizycznie jest u Ciebie w lokalu** (aplikacja sprawdza jego lokalizację GPS, żeby nie można było aktywować rabatu z domu). Dostaje na ekranie kod QR i krótki kod literowy (np. "A7K-9MX").

### Krok 4 — Kelner skanuje kod

Twój kelner otwiera **Talewalk Partner** (prosta aplikacja na tablecie kasowym lub telefonie). Skanuje QR z ekranu gościa. Wpisuje wartość zamówienia (np. 80 zł). Naciska "Potwierdź".

System od razu pokazuje:
- Klientowi rabat 8 zł (10% × 80 zł)
- Tobie informację: "Wizyta zarejestrowana, prowizja Talewalk: 8 zł"

Kelner finalizuje rachunek normalnie, z odjętym rabatem.

### Krok 5 — Gość płaci normalnie

Klient płaci kelnerowi tak jak zawsze — gotówką lub kartą. **Pieniądze idą bezpośrednio do Ciebie, nic nie przechodzi przez Talewalk.**

---

## Ile to kosztuje?

### Opłaty stałe — **zero zł**

Bez abonamentu, bez opłaty wejściowej, bez kary za rezygnację. Nie zarabiamy, jeśli Ty nie zarabiasz.

### Prowizja — 10% od każdej potwierdzonej wizyty

Płacisz tylko za realne wizyty, które przyszły z Talewalk. Każdą można zweryfikować w swoim panelu (kto, kiedy, jaka kwota zamówienia).

### Rozliczenie

Raz w miesiącu (np. pierwszego dnia miesiąca) dostajesz od nas fakturę VAT na zsumowaną kwotę prowizji za poprzedni miesiąc. Płacisz zwykłym przelewem w ciągu 14 dni.

**To jest standardowa faktura między firmami — Twoja księgowa zna ten model.** Faktura jest dla Ciebie kosztem (możesz odliczyć VAT i zaliczyć w koszty uzyskania przychodu).

---

## Konkretny przykład — restauracja "Weranda Café"

Załóżmy, że Twoja restauracja podpisuje umowę z Talewalk. Średnia wartość rachunku gościa: 80 zł.

**Pierwszy miesiąc (czerwiec):**
- 12 turystów aktywowało rabat w Twoim lokalu
- Średnia wartość ich rachunków: 75 zł (turyści często zamawiają więcej)
- **Twój obrót z tych wizyt: 900 zł**
- Rabat klienta (suma): 90 zł (klienci faktycznie zapłacili 810 zł)
- **Prowizja Talewalk: 90 zł** (10% od 900 zł brutto)
- Faktura: 90 zł netto + 23% VAT = **110,70 zł brutto**

**Twoja kalkulacja:**
| Pozycja | Kwota |
|---|---|
| Obrót z wizyt Talewalk | +900 zł |
| Rabat dla klientów | −90 zł |
| Prowizja Talewalk (z VAT) | −110,70 zł |
| **Twój zysk dodatkowy** | **+699,30 zł** |

A pamiętaj — to są klienci których byś inaczej **nie miał**. To nie zabieranie sobie własnych gości, to nowi ludzie sprowadzeni przez aplikację.

---

## "A jeśli klient przyszedłby do mnie i tak, bez Talewalk?"

To nasze największe pytanie do Ciebie podczas rozmowy walidacyjnej. Mamy kilka odpowiedzi:

1. **Aplikacja jest darmowa dla turysty.** Pobiera ją *zanim* przyjedzie do Bydgoszczy — najczęściej w pociągu/aucie albo w hotelu pierwszego wieczoru. Decyduje o trasie zwiedzania na podstawie podpowiedzi aplikacji.

2. **Pokazujemy oferty tylko gdy turysta nie zna lokalu.** Czyli nie pokażemy mu Twojego lokalu, jeśli już wpisał Twój adres w mapy. Aplikacja pomaga **odkrywać** nowe miejsca, a nie pokazywać drogę do znanego celu.

3. **Możesz w każdej chwili wyłączyć ofertę.** Np. w weekendy gdy i tak masz pełno — wstrzymujemy rabaty na sobotę-niedzielę. Włączasz w niedzielę wieczór, aktywne od poniedziałku.

4. **Limity dziennych aktywacji.** Jeśli wiesz że Twój lokal mieści 50 osób — ustawiasz "max 10 aktywacji dziennie". Nie będziemy generować większego ruchu niż obsłużysz.

5. **Audyt po pierwszym miesiącu.** Jeśli widzisz że klienci by tak czy inaczej przyszli — rezygnujesz. Bez kar.

---

## Co musisz zrobić żeby zacząć?

### Wariant A — z naszą pomocą (zalecane na start)

1. **Spotkanie 30 minut.** Przychodzimy do Ciebie, pokazujemy aplikację, odpowiadamy na pytania.
2. **Podpisanie umowy.** Krótka, 2-3 strony. Główne warunki: 10% prowizja, miesięczne fakturowanie, rezygnacja w każdej chwili z 14-dniowym wypowiedzeniem.
3. **Konfiguracja oferty.** My ustawiamy w systemie: typ rabatu (procentowy/kwotowy), godziny ważności, limity.
4. **Szkolenie kelnerów (15 minut).** Pokazujemy jak skanować QR. Jak weryfikować że klient nie zeskanował tego samego dwa razy.
5. **Naklejka na drzwi.** "🎟 Akceptujemy Talewalk — 10% dla turystów" (zwiększa widoczność, pomaga klientom rozpoznać partnerów).

**Czas od pierwszego spotkania do pierwszej wizyty: 3-7 dni.**

### Co Ty musisz dostarczyć?

- **Dane firmy** (NIP, adres, dane kontaktowe).
- **Tablet, telefon lub laptop** z dostępem do internetu dla kelnerów (mogą używać już istniejącego sprzętu kasowego — nasza aplikacja działa w przeglądarce).
- **Konto bankowe firmowe** (na fakturach od nas).
- **5 minut tygodniowo** żeby spojrzeć w swój panel — sprawdzić ile wizyt, czy nie ma nieprawidłowości.

---

## Co dostajesz?

### Panel partnera (przeglądarka)

Logujesz się na `partners.talewalk.com`, widzisz:

- **Liczba wizyt** dzisiaj / w tym tygodniu / w tym miesiącu
- **Łączna wartość zamówień** klientów Talewalk (np. "12 450 zł w czerwcu")
- **Twoja prowizja do zapłaty** (np. "1 245 zł — faktura wystawiona 1 lipca")
- **Lista wizyt** z datą, godziną, kwotą zamówienia, kwotą rabatu (możesz weryfikować z paragonami)
- **Edycja oferty** — zmień procent, godziny, limity, wstrzymaj/wznów

### Aplikacja dla kelnerów

Działa w przeglądarce (Chrome, Safari na iPad-zie itp.) lub jako prosta aplikacja na telefonie.

- Login PIN-em (każdy kelner ma swój 4-cyfrowy PIN)
- Skanowanie kodu QR z ekranu klienta
- Lub ręczne wpisanie 8-znakowego kodu (jeśli kamera nie działa)
- Wpisanie kwoty zamówienia
- Potwierdzenie

### Wsparcie

Pierwsze 3 miesiące dzwonisz bezpośrednio do mnie (Paweł Kwiecień, +48 ... ...). Telefon w godz. 9-19, pn-sb. Później dedykowany opiekun klienta.

Wszystkie spory rozstrzygamy w 48h — np. klient twierdzi że nie był u Ciebie, partner twierdzi że klient anulował zamówienie.

---

## Najczęstsze obawy partnerów

### "Kelnerzy nie ogarną kolejnego systemu"

Skanowanie kodu QR i wpisanie kwoty zajmuje **15 sekund**. Mniej niż czas potrzebny na wybicie paragonu na kasie. Możemy pokazać Wam aplikację na żywo zanim podpiszemy umowę.

### "Klienci będą oszukiwać — pokażą zdjęcie cudzego QR"

Każdy QR jest:
- **Jednorazowy** — po zeskanowaniu nie da się go użyć drugi raz
- **Ważny tylko 15 minut** — po tym czasie wygasa
- **Wygenerowany TYLKO gdy klient jest u Ciebie** (GPS sprawdza lokalizację, ≤50m od Twojego adresu)
- **Powiązany z konkretnym kontem klienta** w aplikacji

Nie można pokazać cudzego screenshota i dostać rabat — system to wyłapie.

### "Co jeśli klient anuluje zamówienie po skanowaniu?"

W panelu masz przycisk **"Oznacz jako zwrot"** dostępny 48h od wizyty. Klikasz, podajesz powód, prowizja jest skorygowana w fakturze (lub w następnym cyklu). Klient dostaje informację że jego rabat został cofnięty.

### "Nie chcę żeby kelnerzy mieli wgląd w mój obrót"

Aplikacja dla kelnerów pokazuje **tylko bieżącą wizytę**. Panel zarządczy z liczbami obrotów ma osobne logowanie (np. tylko Ty + księgowa).

### "Jak mi udowodnicie że klient faktycznie przyszedł z Talewalk?"

W panelu widzisz **każdą wizytę** z dokładnym czasem (godzina aktywacji rabatu + godzina skanu przez kelnera). Możesz porównać z paragonami fiskalnymi. Jeśli któraś wizyta budzi wątpliwości — masz 48h żeby zgłosić spór.

### "A jeśli mnie zaspamują rabatami a klienci nie przyjdą?"

To dla nas pyrrusowe zwycięstwo — generujemy aktywacje, których nie ma na rachunkach, my nie inkasujemy prowizji. **Płacisz tylko za zrealizowane wizyty** (czyli te gdzie kelner skanował QR). Same aktywacje (bez skanu) nie kosztują Cię nic.

### "Co z RODO? Klient wie kto przyszedł?"

W swoim panelu widzisz **imię i pierwszą literę nazwiska** klienta (np. "Paweł K.") — to wystarczy do weryfikacji ze spornym przypadkiem. **Nie widzisz adresu e-mail, numeru telefonu ani adresu zamieszkania**. Klient w naszej aplikacji wyraża zgodę na udostępnienie samego imienia (zgoda jest jednorazowa, dla każdej wizyty osobno).

### "Co z VAT-em? Jak to zaksięgować?"

Twoja księgowa zna ten model. Wy fakturujecie standardową sprzedaż gastronomiczną (jak zawsze). My fakturujemy Was za **usługę marketingu — przyprowadzanie klientów** — to dla Was zwykły koszt uzyskania przychodu z możliwością odliczenia VAT-u. Szczegóły rozliczy księgowa w 5 minut.

### "Czy mogę być w Talewalk + Pyszne.pl + Bookingu jednocześnie?"

Tak. Nie wymagamy ekskluzywności. Każdy z tych kanałów obsługuje inny typ klienta (Pyszne = dostawa, Booking = pokoje, Talewalk = turystyka spacerowa). Możesz testować wszystkie.

---

## Kiedy program rusza?

### Faza 1 — pilotaż w Bydgoszczy

- **5-10 partnerów** z centrum Bydgoszczy (Stary Rynek, Mostowa, Wełniany Rynek)
- **3 miesiące** intensywnej obserwacji — czy turyści korzystają, czy partnerzy są zadowoleni
- **Brak opłat** dla pierwszych partnerów przez pierwszy miesiąc (testujemy razem)
- Spotkania kwartalne z partnerami — co działa, co poprawić

### Faza 2 — skalowanie (po 3 miesiącach udanego pilotażu)

- **30-50 partnerów** w Bydgoszczy
- Pełna automatyzacja — fakturowanie miesięczne przez system
- Samoobsługowy panel — sam dodajesz oferty, edytujesz limity bez kontaktu z nami

### Faza 3 — inne miasta (po roku stabilnej pracy w Bydgoszczy)

- Toruń, Gdańsk, Wrocław, Kraków — w zależności od popytu
- Integracje z popularnymi kasami fiskalnymi (Bookwise, iPOS) — rabat auto-aplikowany przez kasę

---

## Pytania od nas do Ciebie

Jeśli rozważasz program, pomóż nam to walidować. W 15-minutowej rozmowie chcielibyśmy się dowiedzieć:

1. **Ile gości tygodniowo to "turyści" w Twoim szacunku?** (rezydenci miasta vs przyjezdni)
2. **Korzystałeś już z platform partnerskich** typu Booking, Pyszne, Klook? Co działało, co nie?
3. **Jaka prowizja byłaby dla Ciebie do przyjęcia** — 5%, 10%, 15%? Co decyduje?
4. **Co byś chciał widzieć w panelu** żeby mieć poczucie kontroli?
5. **Jakie obawy** masz, że może coś nie zadziałać?

To rozmowa **eksploracyjna, niezobowiązująca**. Nie sprzedajemy Ci niczego. Chcemy zbudować program który ma sens dla obu stron — Twoja perspektywa jest dla nas najcenniejsza.

---

## Kontakt

**Paweł Kwiecień** — Talewalk, Webplanet
- Email: pkwiecien13@gmail.com
- Telefon: na życzenie (podaj swój — oddzwonię)
- Spotkanie w Twoim lokalu w Bydgoszczy: pn-pt 10:00-18:00

---

## Dodatkowe materiały (dla zainteresowanych)

- **Strona Talewalk:** (placeholder — w budowie)
- **Demo aplikacji turystycznej:** mogę pokazać na żywo na tablecie podczas spotkania
- **Lista miejsc w Bydgoszczy w bazie Talewalk:** ok. 80 atrakcji, restauracji i ciekawych miejsc w obrębie centrum, rośnie tygodniowo
- **Wersja techniczna dokumentu** (dla działu IT, jeśli interesuje): [`../partner-program.md`](../partner-program.md)

---

> **Status dokumentu:** wersja **0.1 — wstępna**. Program partnerski jest w fazie projektowania, nie został jeszcze uruchomiony. Ten dokument jest podstawą do rozmów z potencjalnymi partnerami w Bydgoszczy (faza walidacji). Konkretne warunki (prowizja, terminy, limity) mogą się jeszcze zmienić w zależności od uwag partnerów.
