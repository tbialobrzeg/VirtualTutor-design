# VirtualTutor — R3 prototype (macOS)

**Status: proposed_revision.** Nie jest jeszcze zaakceptowane przez Tomka.

## Zakres R3

Kompletny, klikalny prototyp macOS aplikacji VirtualTutor: powitanie, wybór tutora, onboarding (mikrofon, rozpoznawanie mowy, wybór głosów, podsumowanie), rozmowa z korektą i różnicą dialektową, globalny przełącznik wariantu US/UK, „Nowa rozmowa"/„Kontynuuj rozmowę", sygnał postępu, oraz reprezentatywne stany błędów.

## Viewport i workarea

- `app-viewport`: 1280 × 960 px (treść poniżej natywnego paska tytułu macOS — pasek nie jest częścią tego pliku).
- `app-workarea`: 1180 × 860 px, margines górny 40px, marginesy boczne po 50px przy szerokości referencyjnej, wyśrodkowany poziomo, nie centrowany pionowo.
- Bez zależności od `90vh` — wysokość workarea nie zależy od wysokości viewportu.

## Obsługiwany zakres rozmiarów

Zweryfikowano zachowanie geometrii przy 1280×960 (referencyjny), 1440×1000 i 1600×1200: workarea pozostaje dokładnie 1180×860, margines górny 40px, wyśrodkowanie poziome zachowane — rośnie wyłącznie otaczające tło. Responsywność poniżej 1280×960 jest poza zakresem R3 (osobna przyszła rewizja).

## Named states

35 stanów, każdy deterministycznie osiągalny przez `window.__vtDebug.setState(...)` / `window.__vtDebug.goToWizardState(kind, extra, plan)` — mechanizm developerski, niewidoczny w normalnym użyciu aplikacji.

Grupy: Powitanie (1) · Wybór postaci (1) · Onboarding — wariant, mikrofon (intro/aktywny/aktywny-cicho/wynik×3), rozpoznawanie mowy (intro/aktywny/wynik×2), dostępność STT×3, głos kobiecy/męski×3, podsumowanie (20) · Błędy — brak uprawnień mikrofonu, urządzenie nieobsługiwane, brak uprawnień STT, brak modelu językowego, pusty wynik, usługa niedostępna, nieznany błąd, oczekiwanie na ustawienia (8) · Rozmowa — pusta/wysłana wiadomość/korekta otwarta-zwinięta/ślad zmiany wariantu/potwierdzenie nowej rozmowy (6) · Sygnał postępu (1).

## Konwencja data-testid

Semantyczny kebab-case opisujący znaczenie (nie wygląd): `app-viewport`, `app-workarea`, nagłówki (`welcome-headline`, `characters-heading`…), etykiety (`mic-active-status`, `stt-intro-kicker`…), przyciski (`welcome-start`, `mic-check-stop`, `voice-confirm`…), karty (`tutor-tile-{id}`, `voice-option-{id}`…), mierniki wraz z pojedynczymi elementami (`mic-meter`, `mic-meter-bar-{index}`…), komunikaty (`mic-error-no-signal`, `active-demo-label`…), dymki rozmowy (`chat-bubble-greeting/user/reply`), karta korekty (`correction-toggle/detail/wrong/right/explanation`), różnica dialektowa (`dialect-note/-label/-text`), ślad zmiany wariantu (`variant-switch-note`), postęp (`progress-heading`, `progress-dot-{n}`), modal potwierdzenia (`new-conversation-confirm`, `new-conv-confirm-title/body`). Identyfikatory są stabilne między stanami i unikalne w obrębie każdego wyrenderowanego stanu; elementy powtarzalne (kafle tutorów, opcje głosów) mają stabilny identyfikator domenowy (imię/id tutora, id głosu) zamiast przypadkowego numeru narzędzia.

## Znane ograniczenia prototypu

- Miernik poziomu głosu (mikrofon i rozpoznawanie mowy) jest symulowany losowo — docelowo podłączony do rzeczywistego pomiaru audio.
- Lista głosów (Ava, Evan, Kate, Daniel…) to fikcyjny, przykładowy katalog demonstracyjny — nie prawdziwy katalog macOS.
- Responsywność poniżej 1280×960 nieprojektowana w tej rewizji.
- `window.__vtDebug` to narzędzie deweloperskie do nawigacji po stanach — nie jest częścią produkcyjnego zachowania aplikacji.

## SHA-256 (VirtualTutor.dc.html)

`f2836573b8e5eda55966602f7bf6cd132c69949e28da4160715a1fabf1258bec`
