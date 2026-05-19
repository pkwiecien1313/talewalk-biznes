# Plan realizacji Talewalk — priorytety i podział ról

> **Dokument operacyjny dla zespołu dwuosobowego.** Konsoliduje strategię z [`../strategy.md`](../strategy.md), walidację z [`action-plan-validation.md`](action-plan-validation.md), marketing z [`marketing-plan.md`](marketing-plan.md) i program partnerski z [`../partner-program.md`](../partner-program.md) w jedną mapę "co robimy, kto robi, w jakiej kolejności".
>
> **Status:** wersja **0.1 — draft przed walidacją partnerów**. Aktualizujemy po pierwszych 4 tygodniach rozmów.
>
> **Dla kogo:** osoba dołączająca do projektu (marketing + sprzedaż partnerów). Również dla Pawła jako punkt orientacyjny w którą stronę idzie cały projekt.

Sporządzono: 2026-05-20.

---

## 1. W skrócie — co budujemy i dla kogo

**Talewalk** to aplikacja mobilna dla turystów odwiedzających Bydgoszczę:
- Mapa miasta z polecanymi miejscami (atrakcje, restauracje, kawiarnie, muzea)
- Planowanie spaceru / wycieczki na 1-3 godziny
- **Głosowy asystent AI** który odpowiada na pytania w trakcie zwiedzania (kluczowy wyróżnik wobec Google Maps + Gemini)
- **Rabaty u partnerów** — turysta dostaje 10% zniżki w lokalach które dołączyły do programu

**Model zarobku:** prowizja 10% od potwierdzonych wizyt u partnerów (faktura raz w miesiącu). Aplikacja darmowa dla turysty.

**Cel realny w pierwszym roku po premierze:** 1500-4000 aktywnych użytkowników miesięcznie, 30-50 partnerów, dochód miesięczny 4-8 tys zł netto (na utrzymanie jednej osoby + częściowo drugiej).

---

## 2. Zespół i podział obowiązków

> **Model współpracy (aktualnie):** **partnerstwo**, nie zatrudnienie. Oboje (Paweł + Daniel) pracują **bez wynagrodzenia** na tym etapie. Talewalk to nasz wspólny projekt rozwojowy, bez zobowiązań finansowych żadnej ze stron. Gdy pojawi się stabilny przychód — przekształcamy w formalną współpracę (umowa o współpracy / udziały w spółce / wynagrodzenie według ustaleń). Do tego czasu wszystko opiera się na zaufaniu i wspólnym interesie.

### Paweł Kwiecień — produkt + technologia + granty

**Główne odpowiedzialności:**
- **Produkt i kod** — pełen rozwój aplikacji (Ionic Vue 3, AI Live Companion, integracje, AI, audio)
- **Kwestie techniczne** — architektura, baza danych, hosting, bezpieczeństwo
- **Granty** — pisanie wniosków (MKiDN, PARP, RPO), kontakty z Lokalnym Punktem Informacyjnym Funduszy Europejskich
- **Strategiczne decyzje produktowe** — co budujemy, w jakiej kolejności, jak monetyzujemy
- **Ostateczne podpisy umów partnerskich na początku** (pierwsze 5-10 umów, dopóki nie ułożymy procesu i wzoru umowy) — **docelowo finalizacją zajmie się Daniel** samodzielnie
- **Obsługa zgłoszeń technicznych** od użytkowników (po premierze)
- **Konsultacja** dla Daniela w kwestiach strategicznych (nie operacyjnych)

**Niewolno (oddelegowane do Daniela):**
- Pierwsze telefony do partnerów
- Wizyty osobiste u partnerów (poza wyjątkami: bardzo duzi partnerzy, pierwsze spotkanie nowego typu)
- Media społecznościowe
- Cotygodniowe wysyłki do prasy
- Spotkania z Bydgoskim Centrum Informacji Turystycznej i podobnymi instytucjami (mogę towarzyszyć przy pierwszym, dalej Daniel sam)

### Daniel Przybyszewski — marketing + sprzedaż partnerów + relacje

**Główne odpowiedzialności:**
- **Pozyskiwanie partnerów** — telefony, wizyty osobiste, prezentacja aplikacji, podpisywanie listów intencyjnych. **Pełne umowy:** na początku finalizuje Paweł (pierwsze 5-10 partnerów żeby ułożyć proces + wzór), **docelowo Ty samodzielnie** (po przekazaniu wzoru umowy i procesu)
- **Media społecznościowe** — Instagram, TikTok, Facebook (regularne posty, odpowiadanie na komentarze)
- **Lokalna prasa** — informacje prasowe do redakcji, kontakty z dziennikarzami (Express Bydgoski, TVP Bydgoszcz, Radio Pomorze, portale lokalne)
- **Instytucje turystyczne** — Bydgoskie Centrum Informacji Turystycznej, Wojewódzka Organizacja Turystyczna Kujawsko-Pomorska, ewentualnie Urząd Miasta
- **Hotele i Punkty Informacji Turystycznej** — wizyty osobiste, rozmieszczanie materiałów (naklejki, karty QR), propozycje współpracy
- **Wprowadzenie nowych partnerów** — szkolenie kelnerów, dostarczenie naklejek, pierwsza konfiguracja oferty
- **Wycieczki szkolne** — kontakty z nauczycielami, materiały dla szkół
- **Raportowanie tygodniowe** — co piątek 17:00 krótki raport do Pawła z liczb (wykonane telefony, spotkania, podpisane listy, statystyki społecznościowe)

**Niewolno (do konsultacji z Pawłem):**
- Modyfikacja warunków umowy bez konsultacji
- Obietnice konkretnej liczby wizyt
- Obietnice konkretnej daty premiery
- Podpisywanie pełnych umów partnerskich (tylko listy intencyjne na spotkaniu — pełne umowy finalizuje Paweł)
- Obniżki prowizji nieautoryzowane (standardowa obniżka startowa 8% przez 3 mies dla pierwszych 5 partnerów dozwolona, więcej tylko po uzgodnieniu)
- Decyzje techniczne dotyczące aplikacji

### Wspólne rytm pracy

| Częstotliwość | Co | Czas |
|---|---|---|
| Codziennie (luźno) | Aktualizacja arkusza `Talewalk Sprzedaż — Bydgoszcz` | 5 min |
| Piątek 17:00 | Rozmowa statusowa + KPI tygodniowe | 15-30 min |
| Ostatni piątek miesiąca | Refleksja: co działa, co nie, co zmienić | 60 min |
| Co kwartał | Korekta priorytetów + aktualizacja tego planu | 2-3 godz |

---

## 3. Priorytety — co naprawdę zwiększa szanse powodzenia

Po szczerej analizie szans (~15-25% sukcesu zrównoważonego biznesu, 3-7% dużego sukcesu, 60-70% że nie wyjdzie znaczącego dochodu) — te działania **najmocniej wpływają na te szanse**, więc skupiamy się najpierw na nich.

### Tier 1 — game-changery (robimy od razu, każdy może podwoić szanse)

| # | Działanie | Dlaczego ważne | Kto |
|---|---|---|---|
| 1 | **Działanie zamiast planowania** — telefony w pierwszym tygodniu | Plan bez realnych telefonów nic nie znaczy. Po 4 tygodniach walidacji aktualizujemy plan na podstawie realnych odpowiedzi | Daniel (telefony) + Paweł (przygotowanie) |
| 2 | **AI Live Companion + Aktualności w czasie rzeczywistym w pierwszej wersji aplikacji** | Dwa wyróżniki wobec Google Maps + Gemini (które nie pokazują wydarzeń). Lista wszystkich możliwych wyróżników w sekcji "Game-changery — co buduje przewagę" niżej | Paweł |
| 3 | **Hotele jako kanał użytkowników** — 10 hoteli w pierwszych 2 miesiącach po premierze | Mnożnik akwizycji. Jeden hotel z aktywną promocją = 50-200 turystów miesięcznie | Daniel |
| 4 | **3 granty równolegle** (MKiDN, PARP, RPO) zamiast jednego po drugim | Akceptacja 30-40% na jeden = ~70% szansa że któryś przejdzie z trzech | Paweł |
| 5 | **Zespół 2-osobowy zamiast solo** | Solo nie zbuduje (sprzedaż + kod + marketing + obsługa za dużo dla jednego) | ✓ ZAŁATWIONE (już mamy 2 osoby) |

### Tier 2 — asymetryczne stawki (mniejsze działanie, duży potencjał)

| # | Działanie | Dlaczego ważne | Kto |
|---|---|---|---|
| 6 | **Wycieczki szkolne** — kontakt z 50 szkołami w promieniu 100 km od Bydgoszczy | 10-15% bydgoskich turystów to wycieczki szkolne. Konkurencja słaba | Daniel |
| 7 | **Bydgoskie Centrum Informacji Turystycznej (BCI) jako oficjalny partner** | Instytucjonalna wiarygodność za darmo. 3 punkty informacji + możliwe polecenie na visitbydgoszcz.pl | Paweł (pierwsze spotkanie) + Daniel (operacje) |
| 8 | **Audio-przewodnik** (5-10 tras z syntezą mowy w MVP) | Pozwala pozycjonować się w sklepie jako "audio-przewodnik" (mniej konkurencji) zamiast "aplikacja turystyczna" | Paweł |
| 9 | **Blog SEO** — 1 artykuł tygodniowo, "co zobaczyć w Bydgoszczy", "spacer Brdą" itp. | Google Search to długoterminowy kanał bez konkurencji. Po roku 50 artykułów = pasywne pobrania 24/7 | Daniel (treści) + Paweł (publikacja) |
| 10 | **Toruń jako drugie miasto** — przygotować architekturę, NIE odpalać przed pierwszym rokiem Bydgoszczy | Multi-city w architekturze już jest. Toruń = 2x rynek za 1.3x kosztu | Paweł (gdy czas) |

### Tier 3 — kosmetyczne / niski koszt ale warto

| # | Działanie | Kto |
|---|---|---|
| 11 | 30 recenzji od znajomych w pierwszym tygodniu po premierze | Paweł (lista znajomych) + Daniel (koordynacja) |
| 12 | Współpraca z 1-2 mikroinfluencerami (Bydgoszcz, 10-30k obserwujących) za barter | Daniel |
| 13 | Konkurs fotograficzny na Instagramie ("najlepsze zdjęcie z Talewalk") | Daniel |
| 14 | Mentorzy: PARP Platformy Startupowe, Bydgoszcz Hub, Łukasiewicz | Paweł |

---

## 3a. Game-changery — co buduje przewagę nad Google Maps + Gemini

Bez **realnego wyróżnika** aplikacja przegra z darmowym Google Maps. Poniżej 5 możliwych wyróżników, posortowanych od najmocniejszego do najsłabszego. **Decyzja:** w pierwszej wersji robimy #1 + #3 (małe ryzyko, jasna wartość). Reszta jako rozszerzenia.

### Wybrane do pierwszej wersji (MVP)

| # | Game-changer | Co to | Przewaga nad Google Maps | Koszt / Czas |
|---|---|---|---|---|
| 1 | **AI Live Companion** (głosowy asystent) | Turysta zadaje pytanie głosem: *"Co tu jest ciekawego?"* — odpowiedź Claude'a z lokalnym kontekstem Bydgoszczy + odczyt głosem TTS | Gemini odpowiada generycznie ("Bydgoszcz to miasto..."), nie ma lokalnego kontekstu, nie reaguje na pozycję GPS | 2-3 mies, średni koszt API (do walidacji w pierwszym sezonie) |
| 3 | **Aktualności w czasie rzeczywistym** | Co się dzieje **dziś** w Bydgoszczy: koncert w Operze 19:00, jarmark świąteczny otwarty, wystawa tylko do 22:00, festiwal nad Brdą w sobotę | Google Maps pokazuje godziny otwarcia, ale nie wydarzenia. Kalendarz Bydgoszczy jest rozproszony (strona miasta, Facebook, plakaty) | 2-4 tyg pracy + bieżące utrzymanie bazy (1-2h/tyg dla Daniela) |

### Do rozważenia po pierwszym sezonie (jeśli pierwsze 2 działają)

| # | Game-changer | Co to | Kiedy | Komentarz |
|---|---|---|---|---|
| 2 | **Voice-first walking** (tryb głosowy bez patrzenia w telefon) | Telefon w kieszeni, słuchawki w uszach. Apka sama mówi *"po lewej Spichrze, powiedz 'opowiedz' jeśli chcesz historii"* | Po pierwszym sezonie | Naturalne rozszerzenie #1. Idealne dla seniorów, rodzin z dziećmi, fotografów |
| 4 | **AR — przeszłość Bydgoszczy nałożona na rzeczywistość** | Turysta celuje kamerą na Stary Rynek, widzi "tu w 1900 stała kamienica X", postacie z epoki | Po grancie MKiDN | Najmocniejszy "wow", świetny do mediów społecznościowych, ale wymaga finansowania (~10-30k zł treści + 3-6 mies dev) |
| 5 | **Treści od lokalnych mieszkańców** (mini-podcasty 30-90 sek) | "Cześć, jestem Magda, mieszkam tu 30 lat, polecam piekarnię na ulicy X" — 50-100 nagrań od prawdziwych ludzi | Stała aktywność marketingowa | Autentyczność jakiej nie ma Google. Daniel może to organizować jako budowanie społeczności |

### Co NIE jest game-changerem (mimo że ładnie brzmi)

- ❌ Lepsze ikony POI — kosmetyka, nie wpływa na decyzję turysty
- ❌ Tryb ciemny — wymóg podstawowy, nie wyróżnik
- ❌ Lepszy algorytm planowania trasy — Google Maps ma lepszy, nie ma sensu konkurować technicznie
- ❌ Więcej miejsc na mapie — Google Maps ma więcej i zawsze będzie miał

### Dlaczego AI + Aktualności w czasie rzeczywistym (a nie AR) na początek

- **AR jest najmocniejszy**, ale wymaga grantu MKiDN który może nie przyjść w pierwszej rundzie
- **AI + Aktualności są wystarczające** żeby uzasadnić pobranie aplikacji ("po co mam pobrać Talewalk skoro mam Google Maps?" — bo tylko Talewalk wie co się dzieje dziś + odpowie głosem na pytania)
- **Jeśli te dwie funkcje nie wystarczą do osiągnięcia 1500+ aktywnych miesięcznie w pierwszym sezonie** — wtedy wiemy że problem jest głębszy niż brak fosy konkurencyjnej i AR nie pomoże

---

## 4. Fazy realizacji (bez sztywnych dat — kolejność i zależności)

### Faza 0 — Pierwsze 4 tygodnie: walidacja partnerów + wprowadzenie zespołu

**Cel:** dwie rzeczy w tej fazie — (a) zwalidować że model partnerski działa w Bydgoszczy, (b) wprowadzić drugą osobę żeby mogła samodzielnie pracować.

**Wynik mierzalny:** **5+ podpisanych listów intencyjnych** OR jasna decyzja o porzuceniu / przebudowie pomysłu.

#### Działania Pawła

- [ ] **Tydzień 1:** wprowadzenie Daniela — przekazanie wszystkich dokumentów, dostęp do narzędzi (Google Sheets, konto na Instagram, telefony), pierwsza wspólna rozmowa (90 min)
- [ ] **Tydzień 1:** sprawdzenie aktualnych naborów PARP Platformy Startupowe w regionie kujawsko-pomorskim
- [ ] **Tydzień 2:** umówienie konsultacji z Lokalnym Punktem Informacyjnym Funduszy Europejskich w Toruniu (tel. 56-621-25-95, bezpłatna)
- [ ] **Tydzień 2:** sprawdzenie najbliższego naboru MKiDN (terminy, dokumenty wymagane)
- [ ] **Tydzień 1-4:** dokończenie KAN-13 (w toku, branch `feat/kan-13-navigation-actions`)
- [ ] **Tydzień 2-4:** rozpoczęcie prototypu AI Live Companion — Claude Haiku 4.5 + OpenAI TTS, 5-10 pytań / dzień bezpłatnie
- [ ] **Tydzień 4:** wspólnie z Danielem: punkt decyzyjny (idziemy / przebudowujemy / porzucamy)

#### Działania Daniela

- [ ] **Tydzień 1:** zapoznanie się z dokumentami w kolejności: `roadmap.md` (ten) → [`../strategy.md`](../strategy.md) → [`partner-program-biznes.md`](partner-program-biznes.md) → [`partner-program-sprzedaz.md`](partner-program-sprzedaz.md) → [`marketing-plan.md`](marketing-plan.md)
- [ ] **Tydzień 1:** wybór 10-15 partnerów z listy w `action-plan-validation.md`, uzupełnienie arkusza `Talewalk Sprzedaż — Bydgoszcz` (numery, e-maile, godziny otwarcia)
- [ ] **Tydzień 1-2:** pierwsze 3-5 telefonów (skrypt: `partner-program-sprzedaz.md` sekcja 5.1)
- [ ] **Tydzień 2:** spotkanie z Bydgoskim Centrum Informacji Turystycznej — propozycja nieformalnej współpracy (Paweł towarzyszy)
- [ ] **Tydzień 2:** założenie kont @talewalk_bydgoszcz na Instagram, TikTok, Facebook
- [ ] **Tydzień 2-3:** pierwsze posty społecznościowe — narracja "buduję aplikację dla Bydgoszczy", krótkie filmiki z miejscami
- [ ] **Tydzień 3:** kolejne 3-5 telefonów + przygotowanie 2-3 wizyt osobistych w lokalach które wykazały zainteresowanie
- [ ] **Tydzień 3-4:** wizyty osobiste z prezentacją aplikacji (Paweł towarzyszy przy pierwszej żeby pokazać jak prowadzi rozmowę)
- [ ] **Tydzień 4:** prośba o podpisanie listu intencyjnego po każdej pozytywnej wizycie
- [ ] **Każdy piątek:** raport tygodniowy do Pawła (15 min)

#### Punkt decyzyjny (koniec tygodnia 4)

| Wynik | Decyzja | Co dalej |
|---|---|---|
| 5+ podpisanych listów intencyjnych | Idziemy w ścieżkę B (model prowizyjny) | Przejście do Fazy 1 — pre-launch |
| 2-4 listy intencyjne | Wynik niejednoznaczny | Przebudowa modelu (rozważyć ścieżkę C: hybrydową), kolejny tydzień rozmów z innymi pytaniami |
| <2 listy intencyjne | Walidacja negatywna | Poważnie zastanowić się czy w ogóle aplikacja w tym kształcie ma sens. Powrót do ścieżki A (subskrypcyjnej) lub porzucenie pomysłu |

### Faza 1 — Pre-launch (po punkcie decyzyjnym, 2-4 miesiące)

**Cel:** aplikacja gotowa na sezon turystyczny (szczyt maj-wrzesień). 20-35 partnerów łącznie. AI Live Companion działa. Pierwsza wzmianka w prasie.

**Wynik mierzalny:** wszystko gotowe na premierę, lista oczekujących partnerów, materiały rozmieszczone w lokalach.

#### Działania Pawła

- [ ] Dokończenie pierwszej wersji produkcyjnej (MVP techniczny)
- [ ] AI Live Companion zintegrowany w aplikacji (głosowe pytania o miejscach)
- [ ] Aplikacja zarejestrowana w App Store + Google Play (wstępne wpisy)
- [ ] Strona internetowa talewalk.com (jednostronicowa)
- [ ] Złożenie wniosku PARP Platformy Startupowe (jeśli otwarty nabór)
- [ ] Rozpoczęcie pisania wniosku MKiDN (2-4 mies przed corocznym deadline listopad/grudzień)
- [ ] Współpraca z Bydgoskim Centrum Informacji Turystycznej (formalizacja, materiały dla Punktów IT)

#### Działania Daniela

- [ ] Pozyskanie kolejnych 15-25 partnerów (do łącznie 20-35 podpisanych)
- [ ] Druk i rozmieszczenie naklejek "Akceptujemy Talewalk" w lokalach partnerskich
- [ ] Wizyty w **10 hotelach** (Holiday Inn, Mercure, Park Hotel, City Park, Słoneczny Młyn, hostele) — przedstawienie aplikacji + karty QR + propozycja prowizji 5 zł za polecone pobranie
- [ ] Lista 50 szkół podstawowych z okolicy (Bydgoszcz, Toruń, Inowrocław, Włocławek) — przygotowanie krótkiego materiału "Talewalk dla nauczycieli organizujących wycieczki"
- [ ] Regularne posty społecznościowe (3-4× tygodniowo)
- [ ] Wysyłka informacji prasowej do 15 redakcji 2-3 tygodnie przed premierą
- [ ] Telefon do 3 najważniejszych dziennikarzy (Express Bydgoski, TVP Bydgoszcz, Bydgoszcz.Wyborcza)
- [ ] Pierwsze artykuły blogowe na talewalk.com (SEO) — 5-10 artykułów przed premierą

### Faza 2 — Premiera i pierwszy sezon turystyczny (3-4 miesiące)

**Cel:** **realna walidacja w terenie**. Pierwsze przychody z prowizji. Pierwsze poprawki produktu na podstawie zgłoszeń.

**Wynik mierzalny:** 1500-3000 aktywnych użytkowników w peak, 200-500 wizyt potwierdzonych u partnerów, średnia ocena w sklepach 4.3+, 3-5 wzmianek prasowych.

#### Działania Pawła

- [ ] Reagowanie na każdą recenzję w sklepie (każda odpowiedź zwiększa ranking)
- [ ] Cotygodniowe poprawki produktu na podstawie zgłoszeń
- [ ] Finalizacja wniosku MKiDN i złożenie
- [ ] AI Live Companion — analiza kosztów (Claude API + TTS), optymalizacja (cache podobnych pytań)
- [ ] Pierwsze rozliczenia partnerów (faktury miesięczne)

#### Działania Daniela

- [ ] Kolejne 20-30 partnerów (do łącznie 50-70 — koniec fazy 2)
- [ ] Regularne treści społecznościowe (3-4× tygodniowo) + odpowiadanie na komentarze
- [ ] Druga fala kontaktów z mediami (z realnymi liczbami z pilotażu)
- [ ] Pierwsza współpraca z mikroinfluencerem (Instagram, Bydgoszcz)
- [ ] Monitoring KPI tygodniowo (arkusz `Talewalk — wskaźniki`)
- [ ] Wprowadzanie nowych partnerów (szkolenie kelnerów, dostarczanie naklejek)
- [ ] Wycieczki szkolne — pierwsze kontakty z nauczycielami

### Faza 3 — Sezon niski + przygotowanie na drugi sezon (4-5 miesięcy)

**Cel:** utrzymanie aktywności w listopadzie-marcu, ulepszenie produktu, decyzja o drugim mieście (Toruń?).

**Wynik mierzalny:** retencja użytkowników (ile osób wraca po pierwszym pobraniu), spadek do 5-15% pobrań rocznych jest normalny, treści blogowe i pasywne kanały działają.

#### Działania Pawła

- [ ] Refleksja: które kanały marketingowe działały, które nie
- [ ] Dopracowanie AI, audio-przewodnika, eksperymenty z nowymi funkcjami
- [ ] Wyniki MKiDN (3-4 miesiące po złożeniu) → decyzja o przekształceniu na spółkę z o.o.
- [ ] Strategia drugiego miasta — czy Toruń się opłaca, czy zostać przy Bydgoszczy

#### Działania Daniela

- [ ] Treści sezonowe (zima w Bydgoszczy, jarmark świąteczny, walentynki, długie weekendy)
- [ ] Blog SEO — kontynuacja (cel: 50 artykułów po roku)
- [ ] Wycieczki szkolne — drugi sezon (marzec-czerwiec to peak dla nich)
- [ ] Druga fala partnerów — uzupełnienie tych którzy zrezygnowali / dodanie nowych typów (np. atrakcje sezonowe)

### Faza 4+ — Drugi rok i dalej

**Decyzje strategiczne w drugim roku:**
- Toruń jako drugie miasto (jeśli pierwsza Bydgoszcz się sprawdziła)
- Pierwsze kampanie reklamowe płatne (Google Ads, Facebook Ads) jeśli budżet pozwala
- Współpraca z większymi influencerami
- Integracje z kasami fiskalnymi (Bookwise, iPOS) — automatyczny rabat bez ręcznego skanowania

**To nie jest plan na tę chwilę.** Spisujemy żeby pamiętać, ale priorytetem jest pierwszy rok w Bydgoszczy.

---

## 5. Mierzalne cele na każdej fazie

| Faza | Pobrania (kumulatywnie) | Aktywni miesięcznie | Wizyty u partnerów (mies) | Partnerzy | Ocena w sklepach |
|---|---|---|---|---|---|
| **Faza 0** (walidacja) | 0 | 0 | 0 | 5-10 listów intencyjnych | n/d |
| **Faza 1** (pre-launch) | 0-100 (znajomi, testerzy) | 5-20 | 0 | 20-35 listów / pierwsze umowy | 4.0+ (od znajomych) |
| **Faza 2** (pierwszy sezon, koniec) | 1500-3000 | 300-800 | 50-150 | 50-70 podpisanych | 4.3+ |
| **Faza 3** (sezon niski) | 3000-5000 | 200-400 | 30-80 | 50-70 (stabilizacja) | 4.3+ |
| **Faza 4** (drugi sezon) | 8000-20000 | 1500-4000 | 200-500 | 80-120 (jeśli Toruń: dwa razy więcej) | 4.4+ |

---

## 6. Co robimy gdy plan się nie sprawdza

### Walidacja słaba (<2 listów intencyjnych po 4 tygodniach)

**Nie kontynuować z myśleniem "może później pójdzie".** Wracamy do tablicy projektowej. Trzy pytania diagnostyczne (kolejność ważna):

1. **Czy problem jest realny ale my rozwiązujemy go źle?** Może partnerzy nie chcą prowizji 10% (woleliby opłatę stałą), albo nie chcą modelu skanowania QR (woleliby ulotki / kupony papierowe). Wtedy: **zmiana koncepcji rozliczenia**, nie zmiana modelu biznesowego.

2. **Czy w Bydgoszczy nie ma masy krytycznej?** Może 5-10 partnerów to za mało żeby aplikacja miała wartość dla turysty. Może rynek jest po prostu za mały. Wtedy: **zmiana rynku** — np. zacząć od Torunia (większy ruch turystyczny niż się wydaje), Gdańska (sezon dłuższy, więcej zagranicznych), Krakowa (jest masa krytyczna ale konkurencja większa).

3. **Czy w ogóle koncepcja "aplikacja dla turystów + rabaty u partnerów" jest do utrzymania?** Może segment B2C (bezpośrednio turysta) nigdy nie zadziała ze względu na konkurencję z Google Maps. Wtedy: **zmiana modelu** — np. **B2B do organizatorów wycieczek / biur podróży** (Talewalk jako narzędzie dla profesjonalistów którzy planują wycieczki dla swoich klientów), **B2G mini do regionalnych organizacji turystycznych** (Wojewódzka Organizacja Turystyczna kupuje licencję na obsługę regionu).

**Czego NIE robić:**
- ❌ **Wracać do modelu subskrypcyjnego (ścieżki A)** — wszystkie te same problemy z monetyzacją w tej niszy są nadal aktualne (mały LTV turysty, konkurencja z darmowym Google Maps + Gemini, mały polski rynek consumer). Subskrypcja w niszy gdzie commerce nie zadziałał ma jeszcze niższe szanse.
- ❌ Próbować "trochę zmienić ofertę" i dzwonić do tych samych partnerów — to tylko marnowanie reputacji. Jeśli zmieniamy model, dzwonimy do nowych partnerów / w innym mieście.

**Możliwe drogi konstruktywne:**
- Zmiana koncepcji rozliczenia (opłata stała zamiast prowizji, kupony papierowe, inny mechanizm)
- Zmiana rynku (Toruń, Gdańsk — tańsze niż zaczynanie od zera, kod multi-miasto jest gotowy)
- Zmiana segmentu (B2B do biur podróży, B2G do regionalnych organizacji turystycznych)
- Porzucenie pomysłu i powrót do tradycyjnej pracy / klientów Webplanet

### Pierwszy sezon słaby (pobrania <50% planu)

Drugi rok jest **pre-launch'em dla drugiego miasta**, nie skalowaniem Bydgoszczy. Bo dane mówią że sama Bydgoszcz nie wystarczy.

### Wszystkie 3 granty odrzucone

- Konsulting / part-time freelance równolegle (Paweł)
- Tempo wolniejsze, faza 2 może się rozciągnąć o kilka miesięcy
- Daniel na pół etatu zamiast pełnego (do następnej próby grantowej)

### Daniel odchodzi

- Powrót do solo
- Redukcja zakresu (AI Live Companion priorytet absolutny, marketing minimum)
- Decyzja o drugim mieście odwlekana o rok

### AI Live Companion za drogi w utrzymaniu

- Redukcja darmowych pytań (z 10/dzień do 3/dzień)
- Pro+ wprowadzony wcześniej (tylko dla głosowego asystenta)
- Może partnerski Anthropic / OpenAI program startupowy (pierwszy rok zniżki API)

---

## 7. Mapa dokumentów (co czytać kiedy)

### Pierwsze tygodnie — orientacja

1. **Ten dokument (`roadmap.md`)** — co robimy, kto robi
2. **[`../strategy.md`](../strategy.md)** — dlaczego robimy tak a nie inaczej, pełen kontekst strategiczny + słowniczek pojęć
3. **[`../README.md`](../README.md)** — szybki przegląd dokumentów + status projektu

### Działania operacyjne

4. **[`partner-program-biznes.md`](partner-program-biznes.md)** — drukowany materiał do rozmów z partnerami (zostawiasz po spotkaniu)
5. **[`partner-program-sprzedaz.md`](partner-program-sprzedaz.md)** — przewodnik dla Daniela (wzory rozmów, gotowe odpowiedzi, eskalacja)
6. **[`action-plan-validation.md`](action-plan-validation.md)** — 4-tygodniowy plan walidacji + lista konkretnych lokali do obdzwonienia
7. **[`marketing-plan.md`](marketing-plan.md)** — plan pozyskiwania turystów (kanały, kalendarz, budżet)

### Konsultacja / w razie pytań

8. **[`../partner-program.md`](../partner-program.md)** — pełna wersja techniczna programu partnerskiego (dla działu informatycznego partnera, jeśli pyta)
9. **[`../funding-landscape.md`](../funding-landscape.md)** — granty, dotacje, decyzja JDG vs spółka z o.o.
10. **`implementation-plan.md`** — szczegółowy plan techniczny aplikacji (Etapy 1-7). **W osobnym repo z kodem aplikacji** (poza tym repo) — domena Pawła. Jeśli musisz coś znaleźć — pytaj Pawła.

---

## 8. Aktualizacja tego planu

Ten plan jest w **wersji 0.1 (draft przed walidacją)**. Aktualizujemy go:

- **Po fazie walidacji** (~4 tygodnie): wynik liczby listów intencyjnych, decyzja kierunkowa, ew. przebudowa modelu
- **Po premierze** (po pierwszych miesiącach): kalibracja na podstawie realnych pobrań, wizyt, zgłoszeń
- **Co kwartał**: refleksja "co działa, co nie", korekta priorytetów

**Kto aktualizuje:** Paweł na podstawie wspólnej rozmowy z Danielem (ostatni piątek miesiąca, 60 min).

---

## 9. Kontakt w razie wątpliwości

**Paweł Kwiecień**
- E-mail: pkwiecien13@gmail.com
- Codzienna dostępność: w godzinach pracy 9-17

**W razie pytania o:**
- Strategia / pivot / wątpliwości kierunkowe → Paweł, natychmiast
- Wątpliwości w rozmowie z partnerem → Paweł, w trakcie rozmowy SMS-em
- Treść posta społecznościowego → Daniel decyduje, Paweł czyta cotygodniowo
- Decyzja o nowym partnerze (kontrowersyjna) → Paweł, w ciągu 24h
- Awaria techniczna / błąd w aplikacji → Paweł, natychmiast
