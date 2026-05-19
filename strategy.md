# Talewalk — strategy notes

> **Status:** eksploracja, **brak commitmentu**. Dokumentacja techniczna w głównym repo z kodem aplikacji (`talewalk/talewalk-docs/domains/subscription.md`) + ticket KAN-16 nadal odzwierciedlają obecny kierunek (subscription-first). Ten plik to materiał do decyzji, nie zatwierdzony pivot.

Sporządzono: 2026-05-17 po sesji eksploracyjnej z Claude o szansach monetyzacji.

---

## Problem — dlaczego subscription-first może nie działać

Talewalk w obecnym kształcie zakłada model SaaS z trzema planami (Free 5 wycieczek total, Pro 19zł/mies 5 wycieczek/mies + offline + opis głosem, Pro+ 39zł/mies bez limitu + nawigacja głosowa + PDF). Zidentyfikowane ryzyka tego modelu:

- **Niski LTV per user w turystyce.** Turysta = jedno-/dwurazowy użytkownik w roku. Większości wystarczy free tier (5 wycieczek total to dla casual-turysty kilka lat). Konwersja na płatny plan będzie minimalna.
- **Konkurencja z darmowymi alternatywami.** Google Maps + Gemini, Komoot, GuideAlong. AI opisy + TTS jako Pro+ feature to nie killer differentiator w sytuacji gdy bazowy Google Maps jest free i ma rosnące AI features.
- **Multi-city contract nie skaluje treści.** Każde miasto wymaga ręcznego datasetu/treści/lokalnej historii — to wąskie gardło które pochłania całą marżę z subskrypcji.
- **Solo founder + polski rynek consumer.** Żeby utrzymać dev przy cenie 19zł i konwersji 1-2% — potrzeba 50-100k MAU. Bardzo trudne osiągnąć solo w niszowej kategorii bez budżetu marketingowego.
- **Trip mod limits 0/3/5** jako sztuczna bariera nie generuje revenue (tylko frustrację) — to typowy "fake scarcity" który psuje UX bez korzyści finansowej.

---

## Trzy ścieżki monetyzacji

### A) Subscription-first (status quo — szczegóły techniczne w repo z kodem: `talewalk-docs/domains/subscription.md`)

- **Plus:** prosty model, wszyscy go znają, RevenueCat/Stripe support out-of-the-box
- **Minus:** wymaga skali której solo founder w niszy turystycznej nie osiągnie w realnym czasie
- **Realne przychody w 12 mies:** prawdopodobnie 0-2k zł/mies przy dużym wysiłku marketingowym

### B) Free + Commerce-only (marketplace)

- Apka 100% darmowa, brak subskrypcji, brak quota
- Revenue = prowizja od partnerów lokalnych (restauracje, atrakcje, kafejki, sklepy z pamiątkami)
- Mechanizm: turysta widzi w apce "10% rabat u Janka" → pokazuje ekran/QR → backend trackuje wizytę → Talewalk fakturuje partnera za prowizję 10-15% od wartości rachunku
- **Model rozliczeń w MVP (Scenariusz A — patrz `partner-program.md`):** turysta płaci tradycyjnie u kelnera, Talewalk wystawia partnerom faktury B2B raz w miesiącu za usługę marketingu afiliacyjnego (przyprowadzanie klientów). **Bez Stripe Connect, bez licencji MIP** (Mała Instytucja Płatnicza) — wystarczy JDG (Jednoosobowa Działalność Gospodarcza) + zwykłe konto firmowe. Stripe Connect dopiero w Phase 2/3 jako opcjonalny upgrade dla partnerów którzy chcą automatycznych wypłat (Scenariusz B).
- **Plus:** zero friction akwizycji → max userzy → max commission base; partner widzi atrybuowane wizyty; skalowanie przez dodawanie partnerów/miast
- **Minus:** problem chicken-and-egg, czyli "jajka i kury" (bez 20-30 partnerów apka nie ma wartości dla turystów, bez turystów partnerzy nie chcą podpisywać — trzeba bootstrap ręcznie); wymaga czasu na networking; ryzyko nieopłaconych faktur od partnerów (windykacja jak każdy dostawca B2B)
- **Realne przychody w 12 mies (Bydgoszcz, 30 partnerów):** 5-10k zł/mies pasywnie z prowizji

### C) Hybrid: Free + jednorazowy "City Pack" + Commerce

- Free = mapa + planowanie + limited voice (np. 10 pytań/dzień)
- City Pack 8-15 zł jednorazowo per miasto = unlimited voice, offline maps, premium tracks na zawsze
- Plus prowizje od partnerów (jak B)
- **Plus:** bardziej naturalne niż recurring dla turysty na weekendzie ("kupuję bo lecę do Krakowa"); kapitalizuje na intent w momencie planowania podróży; oba revenue streams się wzmacniają
- **Minus:** więcej kodu (in-app purchases czyli zakupy w aplikacji + partner attribution czyli przypisywanie wizyt do partnera + entitlement management czyli zarządzanie uprawnieniami "kto co kupił"); fragmentacja revenue (rozproszenie źródeł przychodu — patrz słowniczek)
- **Realne przychody w 12 mies (Bydgoszcz, 30 partnerów + 200 city packs sprzedanych):** 7-15k zł/mies

---

## Rekomendacja (eksploracyjna, do walidacji)

**Ścieżka B na MVP, ewentualnie C w fazie 2.**

Powód: w turystyce subskrypcja walczy z naturą produktu (jednorazowy użytkownik). Commerce skaluje z tym samym contentem (im więcej turystów, tym więcej partnerów chce wejść). Pro/Pro+ w pierwszym roku nie da realnego revenue — natomiast jeden dobry partner restauracyjny może dać więcej miesięcznie niż 100 free-trial userów.

### Konkretne zmiany w produktowych decyzjach (jeśli pivot zatwierdzony):

- ⏸ **Pro/Pro+ paywall** — wyrzucić z MVP, nie blokować voice/offline z subskrypcją (kod store'a zostawić, nie blokować feature gate'ów)
- ⏸ **Trip mod limits 0/3/5** — wyrzucić, sztuczne ograniczenie bez revenue
- ⏸ **KAN-16 (Subskrypcje + Paywall)** — przesunąć do Etapu 6 lub usunąć ze scope Etapu 1
- ➕ **Partner program** — nowy ticket: admin panel (kto, jaka oferta, prowizja %), attribution layer (warstwa atrybucji — mechanizm potwierdzania że dany klient przyszedł z Talewalk przez QR/screen verification), Stripe Connect onboarding (proces rejestracji partnera w Stripe), revenue dashboard (panel przychodów)
- ➕ **Network 20-30 partnerów w Bydgoszczy** — to nie tech, to czas na osobiste rozmowy z restauratorami/atrakcjami

---

## Pytania walidacyjne ZANIM commitujemy pivot

Trzy proste eksperymenty które kosztują kilka godzin a oszczędzają tygodnie:

1. **Test partnerski.** 5 telefonów do losowych restauracji/kafejek koło Starego Rynku w Bydgoszczy. Pytanie: *"Płacilibyście 10% prowizji za zaatrybułowane wizyty z apki turystycznej, gdzie klient pokazuje QR/screen i dostaje 10% rabatu?"*. Jeśli 3 z 5 powie tak — pivot ma sens. Jeśli 1 z 5 — wracamy do A.
2. **Conversion research.** Sprawdzić publiczne wskaźniki konwersji konkurencji (GPSmyCity, GuideAlong, Detour) na Reddit/SensorTower. Jeśli free→pro < 1% to potwierdza hipotezę że subscription jest słaby model w tej niszy.
3. **Compliance check.** Pogadać z księgową o modelu fakturowania B2B (Scenariusz A) — VAT 23% vs zwolnienie MP (mały podatnik), forma faktury, termin płatności standard 14 dni. Stripe Connect i MIP rozważać dopiero przy upgrade do Scenariusza B (Phase 2/3) — wtedy potencjalny deal-breaker, w MVP nie dotyczy.

---

## Co zostaje bez zmian niezależnie od ścieżki

- **AI Live Companion (głosowy)** — voice questions ("co to za budynek?", "gdzie zjeść tanio?") z Whisper STT + Claude Haiku + OpenAI TTS. Koszt ~$0.01/pytanie. Whisper można zrobić on-device (Capacitor plugin) i zbić koszt do ~$0.005. To jest game-changer feature niezależnie od modelu monetyzacji — działa jako trigger akwizycji.
- **Dynamic Adaptive Mode** — "zmęczyłem się" → skraca trasę, "pada" → kawiarnie z dachem, "z dzieckiem" → place zabaw między POI. Continuous re-planning z LLM. Również niezależne od modelu monetyzacji.

Te dwa features (funkcje) są **moat'em produktu** — czyli fosą konkurencyjną, przewagą trudną do skopiowania przez konkurencję (patrz słowniczek). Subscription vs commerce to decyzja **jak zarabiamy na tej wartości**, nie **jaką wartość dostarczamy**.

---

## Decyzje do zapadnięcia

- [ ] Wykonać 5 telefonów do potencjalnych partnerów w Bydgoszczy (w pierwszym tygodniu walidacji)
- [ ] Uzgodnić z księgową model faktury B2B Talewalk→partner (stawka VAT, termin) — przed wystawieniem pierwszej faktury, ale nie blokuje MVP devu
- [ ] Sprawdzić Stripe Connect + MIP dla JDG (deadline: dopiero przy decyzji o upgrade do Scenariusza B w Phase 2)
- [ ] Decyzja A/B/C — najpóźniej przed startem KAN-16 (data zależna od harmonogramu sprintów)
- [ ] Jeśli B lub C — utworzyć nowy epik "Partner Program" w Jira

---

## Ścieżka E — finansowanie grantami (ortogonalna)

Granty / dotacje to **druga oś** ortogonalna do revenue models (A/B/C). **NIE generują przychodu** — finansują budowę produktu (R&D, content, AI, multimedia, tłumaczenia, accessibility). Mogą działać niezależnie od wybranej ścieżki monetyzacji.

**Top 3 programy dla Talewalk** (szczegóły w `funding-landscape.md`):

1. **MKiDN Dziedzictwo Cyfrowe** — 50-300k, JDG OK, deadline XI-XII corocznie, niska difficulty (self-write), fit 9/10
2. **PARP Platformy Startupowe** — 80k seed + mentoring, JDG OK, bardzo niska difficulty, nabory ciągłe w regionie
3. **RPO Kujawsko-Pomorskie** — 200k-1M, JDG <500k OK, średnia difficulty, ale **wymaga traction** (trakcji — wymiernych dowodów że produkt działa: użytkownicy, partnerzy, revenue; apply po Bydgoszcz validation)

**Decyzja JDG vs sp. z o.o.:**
- Webplanet obecnie JDG, możliwa zmiana na sp. z o.o. (~5-15k jednorazowo + ~15k/rok extra)
- **Zostań JDG** dla MKiDN/PARP/małych RPO — sp. z o.o. nie daje przewagi
- **Zmień na sp. z o.o.** gdy: aplikujesz NCBR (>1M) / pierwszy duży deal partnerski / istotny dochód z commerce
- Trigger praktyczny: zmiana finansuje się z konkretnego revenue/grantu (15k z 150k MKiDN = sensowne)

**Harmonogram:**
- **Faza 1 (równolegle z walidacją partnerów):** apply PARP Platformy Startupowe (jeśli nabór otwarty), zacznij draft MKiDN
- **Najbliższy nabór MKiDN (deadline corocznie listopad/grudzień):** złóż wniosek MKiDN Dziedzictwo Cyfrowe
- **3-4 miesiące po złożeniu MKiDN:** wyniki, decyzja o sp. z o.o.
- **Po przekształceniu na sp. z o.o.:** duże granty (NCBR Szybka Ścieżka, RPO duże nabory) — wymagają sp. z o.o. + traction (wykazanej trakcji)

**Komplementarność z A/B/C/D:**
- E finansuje **budowę produktu** który jest podstawą dla A/B/C/D revenue
- MKiDN może sfinansować content layer Bydgoszczy → wzmacnia ścieżkę B (więcej POI = wartościowsza apka dla partnerów)
- MKiDN może sfinansować WCAG/accessibility → wzmacnia jakość produktu dla wszystkich userów (osoby z niepełnosprawnościami, starsi turyści)
- PARP Platformy Startupowe daje brand "wspierany przez PARP" → wzmacnia wszystkie ścieżki

**Ryzyko:**
- Czas pisania wniosków (40-120h per program) konkuruje z czasem na rozwój produktu
- Vendor lock-in z grantem — co napisałeś musisz dostarczyć, ogranicza pivot flexibility
- Failure rate (30-90% odrzucenia w zależności od programu)

---

## Partner Program — design

Pełen opis programu partnerskiego znajduje się w trzech wersjach (każda dla innego odbiorcy):
- [`partner-program.md`](partner-program.md) — wersja techniczna (architektura, dane, integracje) — dla działu IT
- [`team-onboarding/partner-program-biznes.md`](team-onboarding/partner-program-biznes.md) — wersja dla partnera (restauratora) — bez żargonu, jako materiał do rozmów
- [`team-onboarding/partner-program-sprzedaz.md`](team-onboarding/partner-program-sprzedaz.md) — przewodnik dla sprzedawcy (wzory rozmów, gotowe odpowiedzi, cele tygodniowe)
- [`team-onboarding/roadmap.md`](team-onboarding/roadmap.md) — **master plan zespołu** (priorytety, podział ról Paweł / druga osoba, game-changery, fazy realizacji)

Kluczowe założenia w skrócie:
- **Model revenue (przychodu):** prowizja 10-15% od atrybułowanych transakcji (user pokazuje QR → kelner skanuje → backend rejestruje)
- **3 fazy rollout (wdrażania):** MVP manual (5-10 partnerów, 3 mies) → Beta self-service (30-50 partnerów, 6-9 mies) → Scale multi-city + integracje POS (12+ mies)
- **Stack docelowy (faza 2/3, stos technologiczny):** Firebase Functions + dedykowany Partner Panel (web) + Partner Scanner (PWA — Progressive Web App, aplikacja webowa działająca jak natywna) + opcjonalnie Stripe Connect dla wypłat partnerom. **W pierwszej wersji programu (MVP — Scenariusz A):** bez Stripe Connect, fakturowanie partnerów raz w miesiącu zwykłym przelewem.
- **10 otwartych pytań biznesowych + 7 technicznych** do rozstrzygnięcia przed implementacją

---

## Marketing — pozyskiwanie turystów do aplikacji

Strategia partnerów (kto się reklamuje w aplikacji) to **jedna strona**. Druga strona to **jak sprowadzić użytkowników (turystów) do aplikacji** — bez nich partnerzy nie mają sensu. Plan marketingowy w osobnym dokumencie: [`team-onboarding/marketing-plan.md`](team-onboarding/marketing-plan.md).

Główne kanały (od najtańszych do najdroższych):
- **A. Praktycznie darmowe:** naklejki w lokalach partnerskich, Punkty Informacji Turystycznej, hotele/recepcje, organizatorzy wycieczek
- **B. Tanie:** lokalna prasa, grupy Facebook, Instagram/TikTok organiczny
- **C. Wymagające budżetu (na drugi rok):** reklamy Google / Facebook, mikroinfluencerzy
- **D. Pasywne / długoterminowe:** widoczność w sklepach App Store i Google Play, strona internetowa, polecania od użytkowników

Cele liczbowe pierwszego roku (po premierze): 8-20 tys. pobrań, 1500-4000 aktywnych miesięcznie, średnia ocena 4.3+. Realistyczny budżet bootstrap: **600-4000 zł rocznie**.

---

## Słowniczek pojęć

Sekcja referencyjna dla terminów anglojęzycznych używanych w tym i powiązanych dokumentach. Pierwsze wystąpienie w tekście powinno mieć rozwinięcie inline; tutaj pełne definicje.

### Biznes i monetyzacja

- **Attribution / atrybucja** — przypisanie konkretnej transakcji do kanału marketingowego który ją wygenerował. Tu: identyfikacja że "ten klient przyszedł z aplikacji Talewalk", co uprawnia do prowizji.
- **Bootstrap** — rozwijanie biznesu z własnych środków, bez inwestora zewnętrznego.
- **Booking attribution** — atrybucja w branży hotelarskiej (przypisanie rezerwacji do kanału — Booking.com, Trivago itp.).
- **Cash flow / przepływ gotówki** — kiedy pieniądze faktycznie wpadają na konto vs wychodzą (różne od księgowego zysku, który może istnieć na papierze przy zerowym saldzie).
- **Chicken-and-egg / problem jajka i kury** — klasyczny problem dwustronnych platform: bez jednej strony (np. partnerów) druga (userzy) nie ma wartości, i odwrotnie. Wymaga bootstrap ręcznie — np. sales obchodzi 10 partnerów osobiście zanim platforma cokolwiek "wie".
- **Commission / prowizja** — procent od wartości transakcji który otrzymuje pośrednik. Tu: 10-15% od rachunku gościa w lokalu partnera.
- **Decision gate / punkt decyzyjny** — moment w roadmapie kiedy decydujemy "kontynuujemy / pivotujemy / zabijamy" na podstawie zebranych danych.
- **Entitlement / uprawnienie** — w kontekście subskrypcji: stan informujący "ten user ma dostęp do feature X bo zapłacił". Implementuje się przez Stripe customer + RevenueCat itp.
- **Fixed-fee** — opłata stała (jednorazowa kwota za projekt, nie zależna od użytkowania). Przeciwieństwo: SaaS recurring.
- **KYC (Know Your Customer)** — procedura weryfikacji tożsamości partnera/klienta (skan dowodu, dane firmy) wymagana przez instytucje finansowe i Stripe Connect.
- **LOI (Letter of Intent) / list intencyjny** — niewiążąca prawnie deklaracja zainteresowania współpracą, kładziona przed podpisaniem właściwej umowy.
- **MAU (Monthly Active Users) / miesięczni aktywni użytkownicy** — liczba unikalnych userów którzy używali apki w ciągu 30 dni. Standardowy wskaźnik trakcji.
- **MIP (Mała Instytucja Płatnicza)** — wpis do rejestru KNF (Komisja Nadzoru Finansowego) pozwalający legalnie pośredniczyć w płatnościach klient→sprzedawca. Setup ~10-30k zł + bieżąca compliance.
- **MoR / merchant of record / sprzedawca formalny** — podmiot który formalnie sprzedaje produkt klientowi końcowemu (wystawia paragon/fakturę userowi). Tu istotne czy Talewalk występuje jako sprzedawca rabatu (B2) czy tylko pośrednik (B1).
- **Moat / fosa konkurencyjna** — przewaga którą trudno skopiować konkurencji. Tu: AI Live Companion + Dynamic Adaptive Mode (głosowy asystent + dynamiczne planowanie wycieczki).
- **Opt-in / opt-out** — opt-in: user/partner musi aktywnie wyrazić zgodę żeby dostać feature. Opt-out: feature domyślnie aktywne, user może wyłączyć. Tu: Stripe Connect dla partnerów jako opt-in w Phase 2.
- **Pay-per-result / płatność za wynik** — partner płaci tylko za realne wizyty (vs reklama gdzie płacisz za odsłony bez gwarancji konwersji).
- **Payout / wypłata** — transfer pieniędzy z platformy do partnera (po potrąceniu prowizji platformy).
- **Pivot / zwrot strategiczny** — istotna zmiana kierunku produktu/modelu biznesowego w odpowiedzi na nowe dane z rynku.
- **Refund window / okno zwrotu** — czas w którym partner może oznaczyć transakcję jako zwróconą (np. 48h od wizyty), z konsekwencjami korekty prowizji.
- **SaaS (Software as a Service)** — model gdzie klient płaci cykliczną opłatę (mies/rok) za dostęp do oprogramowania w chmurze.
- **Sales cycle / cykl sprzedażowy** — czas od pierwszego kontaktu z potencjalnym klientem do podpisania umowy. Tu: B2C = 0 dni (turysta klika), B2B partnerzy lokalni = tygodnie.
- **Threshold / próg** — minimalna wartość uruchamiająca akcję (np. payout dopiero gdy uzbierane ≥50 zł).
- **Ticket size / wartość pojedynczej transakcji** — średnia wartość zamówienia. Im wyższy ticket size, tym większa prowizja absolutna przy tej samej stawce procentowej.
- **Traction / trakcja** — wymierne dowody że produkt działa: liczba userów, revenue, growth rate, retention. Wymagana przez większość grantów i inwestorów.
- **Value prop (value proposition) / propozycja wartości** — jedno-dwuzdaniowe wyjaśnienie "co dostaje klient i dlaczego to lepsze niż alternatywy".

### Prawo i finanse w PL

- **JDG (Jednoosobowa Działalność Gospodarcza)** — polska forma prawna jednoosobowego biznesu wpisanego do CEIDG (Centralna Ewidencja i Informacja o Działalności Gospodarczej). Najtańsza w prowadzeniu, najsłabsza w wymiarze odpowiedzialności (właściciel odpowiada całym majątkiem).
- **sp. z o.o. (spółka z ograniczoną odpowiedzialnością)** — polska forma prawna z osobowością prawną, ograniczona odpowiedzialność wspólników. Setup ~5-15k jednorazowo + ~15k/rok extra kosztów księgowości. Wymagana dla niektórych dużych grantów (NCBR) i przetargów publicznych.
- **VAT MP / mały podatnik** — preferencyjny status VAT dla firm o obrotach <2M EUR rocznie, pozwala na uproszczone rozliczenia.

### Techniczne (jeśli nie są standardem branżowym po polsku)

- **API (Application Programming Interface)** — interfejs umożliwiający komunikację między systemami (Talewalk Functions ↔ Stripe ↔ Firestore).
- **CRUD (Create/Read/Update/Delete)** — pełen zestaw operacji na zasobie w bazie (np. partner może tworzyć/edytować/usuwać oferty).
- **MVP (Minimum Viable Product) / produkt minimalnie funkcjonalny** — najmniejsza wersja produktu którą można już oddać do walidacji rynkowej.
- **PWA (Progressive Web App)** — aplikacja webowa zachowująca się jak natywna (instalowalna, działa offline, push notifications).
- **POS (Point of Sale)** — system kasowy w lokalu (Bookwise, iPOS, terminale płatnicze). Integracja z POS = auto-deduct rabatu bez ręcznego wpisywania.
- **reCAPTCHA** — usługa Google weryfikująca że user jest człowiekiem, nie botem.
- **Stack technologiczny / stos** — zestaw technologii którymi system jest zbudowany (frontend + backend + database + hosting).
