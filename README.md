# JAKDZISIAJ.PL

<div align="center">

**Minimalistyczna, czarno-biała strona pogodowa. Bez frameworków. Bez kont. Bez zbędnych dodatków.**

[![HTML](https://img.shields.io/badge/HTML5-vanilla-000000?style=flat-square&logo=html5&logoColor=white)](.)
[![CSS](https://img.shields.io/badge/CSS-vanilla-000000?style=flat-square&logo=css&logoColor=white)](.)
[![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-000000?style=flat-square&logo=javascript&logoColor=white)](.)
[![API](https://img.shields.io/badge/API-Open--Meteo-000000?style=flat-square)](https://open-meteo.com)
[![License](https://img.shields.io/badge/license-MIT-000000?style=flat-square)](LICENSE)
[![Website](https://img.shields.io/badge/website-jakdzisiaj.pl-000000?style=flat-square)](https://jakdzisiaj.pl)

</div>

---

## Co to jest

**[jakdzisiaj.pl](https://jakdzisiaj.pl)** to minimalistyczna strona pogodowa napisana w czystym HTML, CSS i JavaScript.

Projekt korzysta z lokalizacji urządzenia albo ręcznie wybranej miejscowości i pokazuje:

- aktualną temperaturę,
- temperaturę odczuwalną,
- prędkość wiatru,
- temperaturę minimalną i maksymalną,
- pogodę na poszczególne pory dnia,
- prognozę na 10 dni,
- porównanie temperatury z poprzednim dniem.

Interfejs został zaprojektowany od nowa w klasycznej, nowoczesnej estetyce black & white. Poprzedni styl pixel-art został całkowicie usunięty.

---

## Wygląd

Aktualny interfejs stawia na:

- czarno-białą kolorystykę,
- duże, czytelne wartości temperatury,
- minimalistyczne karty,
- cienkie obramowania,
- subtelne cienie,
- prostą typografię systemową,
- responsywny układ na desktopie, tablecie i telefonie,
- brak efektów retro, scanlines i pixel-artu.

Strona nie korzysta z Google Fonts — fonty są pobierane z systemu użytkownika.

---

## Funkcje

- 📍 **Lokalizacja za zgodą użytkownika** — GPS uruchamia się dopiero po kliknięciu „Użyj mojej lokalizacji”
- 🏙️ **Ręczny wybór miejscowości** — użytkownik może korzystać ze strony bez udostępniania lokalizacji
- 🔍 **Wyszukiwarka miejscowości** — wyszukiwanie przez Nominatim / OpenStreetMap
- 🌡️ **Aktualna pogoda** — temperatura, odczuwalna, wiatr, minimum i maksimum dnia
- 🕒 **Pogoda na cały dzień** — rano / południe / wieczór / noc
- 📆 **Prognoza 10-dniowa** — temperatury minimalne i maksymalne
- ↕️ **Porównanie z poprzednim dniem** — cieplej / chłodniej / podobnie
- 🕐 **Zegar na żywo** — aktualizowany co sekundę
- ☰ **Panel boczny** — szybka zmiana miejscowości
- 📱 **Responsive design** — mobile, tablet, desktop
- 🔒 **Privacy-first flow** — brak automatycznego pytania o GPS po wejściu
- 📄 **Polityka prywatności** — osobna strona `privacy.html`
- 🚫 **Brak trackerów** — brak Google Analytics, Meta Pixel i podobnych narzędzi w aktualnej wersji

---

## Flow lokalizacji

```text
Wejście na stronę
        │
        ▼
Ekran wyboru sposobu
        │
   ┌────┴───────────────┐
   │                    │
   ▼                    ▼
Użyj mojej         Wybierz miejscowość
lokalizacji              │
   │                     ▼
   ▼               Lista / wyszukiwarka
Zapytanie
przeglądarki
o dostęp do GPS
   │
┌──┴───────────┐
│              │
▼              ▼
Zgoda        Odmowa / błąd
│              │
▼              ▼
Pobierz      Ekran błędu
pogodę          │
                ▼
         Wybór ręczny
```

Lokalizacja **nie jest pobierana automatycznie**. Funkcja `navigator.geolocation` jest uruchamiana dopiero po świadomym kliknięciu użytkownika.

---

## Prywatność

Projekt został przebudowany tak, aby ograniczyć zbędne połączenia z usługami zewnętrznymi.

Aktualna wersja:

- nie korzysta z Google Fonts,
- nie korzysta z Google Analytics,
- nie korzysta z Meta Pixel,
- nie korzysta z kont użytkowników,
- nie zapisuje historii lokalizacji w swojej bazie,
- nie uruchamia GPS automatycznie po wejściu na stronę.

Po użyciu lokalizacji współrzędne są wykorzystywane do:

1. pobrania pogody z **Open-Meteo**,
2. ustalenia nazwy miejscowości przez **Nominatim / OpenStreetMap**.

Szczegóły znajdują się w pliku:

```text
privacy.html
```

oraz na publicznej stronie polityki prywatności.

Administrator serwisu:

```text
Kasper Tokarz
kontakt@jakdzisiaj.pl
```

---

## Jak uruchomić

```bash
git clone https://github.com/twoj-nick/jakdzisiaj.pl
cd jakdzisiaj.pl
```

Następnie uruchom lokalny serwer, np.:

```bash
python -m http.server 8000
```

i otwórz:

```text
http://localhost:8000
```

Możesz też odwiedzić:

**[https://jakdzisiaj.pl](https://jakdzisiaj.pl)**

> Geolokalizacja w przeglądarce wymaga bezpiecznego kontekstu — HTTPS albo `localhost`.

---

## Stack

| Warstwa | Technologia |
|---|---|
| Markup | HTML5 |
| Styl | CSS Vanilla |
| Layout | Flexbox / Grid / `clamp()` / `@media` |
| Skrypt | Vanilla JavaScript |
| Pogoda | [Open-Meteo API](https://open-meteo.com) |
| Geokodowanie | [Nominatim / OpenStreetMap](https://nominatim.org) |
| Font | System font stack |
| Prywatność | Własna polityka prywatności |
| Hosting | [jakdzisiaj.pl](https://jakdzisiaj.pl) |

Projekt nie wymaga:

- Node.js,
- npm,
- frameworków frontendowych,
- bundlera,
- klucza API do Open-Meteo.

---

## Struktura projektu

```text
jakdzisiaj.pl/
│
├── index.html
│   ├── style strony
│   ├── ekran startowy
│   ├── obsługa lokalizacji
│   ├── wyszukiwarka miejscowości
│   ├── pobieranie danych pogodowych
│   └── renderowanie interfejsu
│
├── privacy.html
│   └── polityka prywatności serwisu
│
├── README.md
│   └── dokumentacja projektu
│
└── LICENSE
    └── licencja MIT
```

---

## Najważniejsze elementy kodu

### `showWelcome()`

Wyświetla ekran startowy z wyborem:

- użycia lokalizacji,
- ręcznego wyboru miejscowości.

GPS nie jest uruchamiany przed kliknięciem użytkownika.

### `tryGPS()`

Uruchamia:

```js
navigator.geolocation.getCurrentPosition(...)
```

i przekazuje uzyskane współrzędne do funkcji pobierającej pogodę.

### `getCityName()`

Wykorzystuje Nominatim do reverse geocodingu:

```text
współrzędne → nazwa miejscowości
```

### `fetchWeather()`

Pobiera dane pogodowe z Open-Meteo.

### `renderWeather()`

Buduje główny widok pogody:

- aktualne warunki,
- temperaturę,
- odczuwalną,
- wiatr,
- pogodę na pory dnia,
- prognozę 10-dniową.

### `showCityPicker()`

Pokazuje ręczny wybór miejscowości oraz wyszukiwarkę.

### `openPanel()`

Otwiera boczny panel szybkiej zmiany lokalizacji.

---

## API

### Open-Meteo

```http
GET https://api.open-meteo.com/v1/forecast
  ?latitude={lat}
  &longitude={lon}
  &hourly=temperature_2m,weathercode,windspeed_10m,apparent_temperature
  &daily=weathercode,temperature_2m_max,temperature_2m_min
  &timezone=auto
  &past_days=1
  &forecast_days=11
```

`past_days=1` jest wykorzystywane do porównania dzisiejszej temperatury maksymalnej z poprzednim dniem.

---

### Nominatim — reverse geocoding

```http
GET https://nominatim.openstreetmap.org/reverse
  ?lat={lat}
  &lon={lon}
  &format=json
  &accept-language=pl
```

Służy do zamiany współrzędnych GPS na nazwę miejscowości.

---

### Nominatim — wyszukiwanie

```http
GET https://nominatim.openstreetmap.org/search
  ?q={query}
  &countrycodes=pl
  &format=json
  &limit=8
  &accept-language=pl
```

Służy do wyszukiwania miejscowości po nazwie.

---

## Responsywność

Interfejs jest przygotowany pod:

- telefony,
- tablety,
- standardowe monitory,
- duże ekrany desktopowe.

Na mniejszych ekranach kolumnowy layout przechodzi w układ pionowy, dzięki czemu prognoza pozostaje czytelna bez poziomego przewijania.

---

## Bezpieczeństwo i prywatność

### Lokalizacja

Lokalizacja urządzenia jest opcjonalna.

Użytkownik może korzystać z serwisu bez udostępniania GPS, wybierając miejscowość ręcznie.

### Dane zewnętrzne

Przy korzystaniu z lokalizacji przeglądarka wykonuje zapytania do:

- Open-Meteo,
- Nominatim / OpenStreetMap.

W związku z tym do tych usług mogą trafiać dane techniczne połączenia oraz współrzędne użyte w zapytaniu.

### Cookies

Aktualna wersja projektu nie ustawia własnych cookies analitycznych ani marketingowych i nie korzysta z systemów reklamowych.

Jeżeli w przyszłości zostaną dodane narzędzia analityczne, reklamowe albo inne niekonieczne technologie zapisujące dane na urządzeniu użytkownika, polityka prywatności i sposób uzyskiwania zgody powinny zostać zaktualizowane.

---

## Changelog

### v2.0.0 — październik 2026

- całkowicie nowy, minimalistyczny black & white design,
- usunięty pixel-art,
- usunięty font Press Start 2P,
- usunięte efekty retro / scanlines,
- nowe nowoczesne karty pogodowe,
- nowe ikony pogodowe,
- poprawione polskie znaki,
- przebudowany ekran startowy,
- GPS uruchamiany dopiero po kliknięciu użytkownika,
- dodany ręczny wybór lokalizacji przed zgodą na GPS,
- dodana polityka prywatności,
- dodana stopka z informacją o dostawcach danych,
- usunięte Google Fonts,
- zachowana obsługa Open-Meteo i Nominatim,
- zachowany responsywny layout.

### v1.4.0 — kwiecień 2025

- usunięta mapa Polski,
- dodana alfabetyczna lista 45 miast,
- naprawiony konflikt `z-index` w hamburger menu,
- panel wyszukiwania dostępny niezależnie od statusu GPS.

### v1.3.0 — kwiecień 2025

- dodany hamburger menu,
- dodany wysuwany panel boczny,
- dodana pikselowa mapa Polski.

### v1.2.0 — kwiecień 2025

- czarno-biały design,
- ręcznie rysowane ikony SVG pixel-art,
- pełny responsive,
- ekran błędu GPS.

### v1.1.0 — kwiecień 2025

- obsługa geolokalizacji,
- ekran wyboru miasta,
- 3-kolumnowy layout,
- dane pogodowe dla pór dnia.

### v1.0.0 — kwiecień 2025

- pierwsza wersja,
- Open-Meteo API,
- Nominatim,
- pixel font,
- prognoza 10-dniowa.

---

## Roadmap

Możliwe kolejne funkcje:

- jakość powietrza,
- wilgotność,
- ciśnienie,
- indeks UV,
- godziny wschodu i zachodu słońca,
- opady godzinowe,
- wykres temperatury,
- zapamiętywanie wybranego miasta lokalnie w przeglądarce,
- tryb ciemny,
- PWA / instalacja strony jako aplikacji.

---

## Licencja

Projekt jest udostępniony na licencji MIT.

Możesz go modyfikować, rozwijać i wykorzystywać zgodnie z warunkami licencji.

---

<div align="center">

<sub>
<a href="https://jakdzisiaj.pl">jakdzisiaj.pl</a>
· pogoda bez zbędnych dodatków
· bez frameworków
</sub>

</div>
