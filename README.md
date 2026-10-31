# ElektroManiacy — demo landing page przewodnika

Prototyp strony zapisu na przewodnik o wyborze termowizora do polowania. Prezentuje ofertę materiału, formularz zapisu, ekran podziękowania oraz popup zachęcający do pozostawienia adresu e-mail.

**Status:** statyczne demo interfejsu. Zapis jest symulowany w JavaScript; repozytorium nie zawiera backendu, integracji mailingowej ani pliku przewodnika.

## Co jest zaimplementowane

- Responsywna strona z makietą przewodnika, korzyściami, sekcją autora i treściami społecznego dowodu słuszności.
- Walidacja adresu e-mail oraz zgody w głównym formularzu.
- Symulowany stan wysyłania i przejście do ekranu podziękowania po 800 ms.
- Popup przy wyjściu kursorem ponad stronę oraz warunkowo po 50 sekundach, jeżeli użytkownik przewinął ponad 40% wysokości dokumentu.
- Zapamiętanie wyświetlenia popupu w cookie `em_popup` przez 14 dni w ścieżce obsługi wyjścia kursorem.
- Animacje ujawniania sekcji przez `IntersectionObserver`.

## Stos i architektura

Całość mieści się w [index.html](index.html): HTML, osadzone style CSS i JavaScript bez frameworka. Nie ma procesu budowania, pakietów npm ani zmiennych środowiskowych.

Przepływ głównego formularza: walidacja → lokalny stan „Wysyłam...” → przełączenie `#landingPage` na `#thankyouPage`. Żaden z tych kroków nie zapisuje kontaktu na serwerze.

Fonty Oswald i Source Sans 3 są pobierane z Google Fonts. Ekran podziękowania zawiera odnośniki do zewnętrznych stron sklepu i mediów społecznościowych.

## Uruchomienie lokalne

Wymagania: Git, Python 3 i współczesna przeglądarka.

```sh
git clone https://github.com/dzwoniar/demo-elektromaniacy.pl.git
cd demo-elektromaniacy.pl
python -m http.server 8000 --bind 127.0.0.1
```

Otwórz [http://127.0.0.1:8000](http://127.0.0.1:8000). Zatrzymanie serwera: `Ctrl+C`. Nie trzeba instalować zależności.

## Struktura i miejsca zmian

```text
.
├── index.html   # landing page, popup, podziękowanie, CSS i JavaScript
└── README.md    # dokumentacja projektu
```

Treści zmienisz w sekcjach HTML, wygląd w `<style>`, a zachowanie formularzy i popupu w końcowym `<script>`. Elementy `#optinForm`, `#exitPopup` i `showThankYou()` wyznaczają główne punkty interakcji.

## Granice demo

Komunikat o wysłaniu materiału jest częścią symulacji — kod nie wykonuje wysyłki e-mail ani pobierania PDF. Formularz popupu sprawdza adres e-mail, ale nie wymaga tej samej zgody co formularz główny. To odrębne ścieżki interfejsu, które trzeba ujednolicić przed rzeczywistą integracją.

Oceny, opinie i obietnice marketingowe są treścią prototypu; repozytorium nie dokumentuje ich weryfikacji ani efektów kampanii.

## Sprawdzenie po zmianach

Nie ma skonfigurowanych testów automatycznych. Sprawdź lokalnie układ mobilny, walidację pustego i błędnego adresu, stan formularza oraz otwieranie i zamykanie popupu. Do powtórnego sprawdzenia ograniczenia wyświetleń usuń cookie `em_popup` dla lokalnego adresu. Używaj fikcyjnych danych w demonstracji formularzy.
