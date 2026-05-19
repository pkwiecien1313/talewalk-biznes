# Talewalk — dokumenty biznesowe i strategiczne

> Repozytorium zawiera dokumenty **biznesowe, strategiczne i marketingowe** projektu Talewalk — aplikacji turystycznej dla Bydgoszczy.
>
> **Repo z kodem aplikacji jest osobne** (prywatne, nie publikowane na GitHub). Tutaj tylko strategia, partnerzy, marketing, granty — wszystko nie związane bezpośrednio z implementacją.

---

## Zespół

- **Paweł Kwiecień** (właściciel Webplanet) — produkt, technologia, granty
- **Daniel Przybyszewski** — marketing, sprzedaż partnerów, relacje

Model współpracy: **partnerstwo bez zatrudnienia** na obecnym etapie (oboje pracują za darmo). Szczegóły w [`team-onboarding/roadmap.md`](team-onboarding/roadmap.md) sekcja 2.

---

## Struktura repozytorium

### Dokumenty główne (kontekst strategiczny)

- [`strategy.md`](strategy.md) — strategia monetyzacji (ścieżki A/B/C/E), rekomendacja, słowniczek pojęć
- [`partner-program.md`](partner-program.md) — design programu partnerskiego, wersja techniczna (architektura, model danych, integracje)
- [`funding-landscape.md`](funding-landscape.md) — mapa grantów (MKiDN, PARP, RPO), decyzja JDG vs sp. z o.o., harmonogram aplikacji

### Pakiet wprowadzający dla Daniela ([`team-onboarding/`](team-onboarding/))

Dokumenty operacyjne — wszystko czego Daniel potrzebuje żeby zacząć pracę. Czytać w kolejności:

1. [`team-onboarding/README.md`](team-onboarding/README.md) — kolejność czytania + zasady
2. [`team-onboarding/roadmap.md`](team-onboarding/roadmap.md) — **master plan zespołu** (priorytety, podział ról, fazy, game-changery)
3. [`team-onboarding/partner-program-biznes.md`](team-onboarding/partner-program-biznes.md) — opis programu dla partnera (drukowany materiał, bez żargonu)
4. [`team-onboarding/partner-program-sprzedaz.md`](team-onboarding/partner-program-sprzedaz.md) — przewodnik dla Daniela (wzory rozmów, gotowe odpowiedzi, eskalacja)
5. [`team-onboarding/action-plan-validation.md`](team-onboarding/action-plan-validation.md) — 4-tygodniowy plan walidacji partnerów + lista lokali do obdzwonienia
6. [`team-onboarding/marketing-plan.md`](team-onboarding/marketing-plan.md) — plan pozyskiwania turystów do aplikacji

---

## Status projektu

- **Faza:** walidacja partnerów (4-tygodniowa) + równolegle dokończenie wersji MVP aplikacji
- **Konkretna data premiery:** niezdefiniowana — zależy od wyniku walidacji partnerów i tempa rozwoju produktu
- **Punkt decyzyjny:** po ~4 tygodniach walidacji — decyzja "idziemy w model prowizyjny" / "przebudowa" / "porzucenie"

Szczegóły w [`team-onboarding/roadmap.md`](team-onboarding/roadmap.md) sekcja 4 "Fazy realizacji".

---

## Co jest poza tym repo

W osobnym, prywatnym repo z kodem aplikacji (`talewalk/talewalk-docs/`) znajduje się:

- `implementation-plan.md` — szczegółowy plan techniczny Etapów 1-7
- `vue3-ddd-guidelines.md` — wytyczne kodu Vue 3 + DDD
- `places-database.md` — techniczna baza miejsc / narzędzie scrapowania
- `domains/` — dokumentacja domen DDD (auth, map, navigation, subscription, trip-planning, history, settings, voice-guide, notifications)
- `plans/` — plany konkretnych ticketów (KAN-5, KAN-8, KAN-11, KAN-13 itp.)

To są dokumenty **dla Pawła** (produkt + kod). Daniel nie potrzebuje do nich dostępu.

---

## Aktualizacja repo

- **Co tydzień:** Daniel raportuje liczby (piątek 17:00 do Pawła), Paweł aktualizuje arkusz wskaźników
- **Co miesiąc:** wspólna refleksja — co działa, co nie, co zmienić. Aktualizacja `roadmap.md` i `partner-program-sprzedaz.md` na podstawie nowych obserwacji
- **Co kwartał:** głębsza korekta priorytetów + aktualizacja celów fazowych

---

## Kontakt

**Paweł Kwiecień** — pkwiecien13@gmail.com (główny)
**Daniel Przybyszewski** — pkwiecien1313@gmail.com (tymczasowo, projektowy)
