```
     ██╗ █████╗ ██╗  ██╗    ██████╗ ███████╗██╗███████╗██╗ █████╗      ██╗
     ██║██╔══██╗██║ ██╔╝    ██╔══██╗╚══███╔╝██║██╔════╝██║██╔══██╗     ██║
     ██║███████║█████╔╝     ██║  ██║  ███╔╝ ██║███████╗██║███████║     ██║
██   ██║██╔══██║██╔═██╗     ██║  ██║ ███╔╝  ██║╚════██║██║██╔══██║██   ██║
╚█████╔╝██║  ██║██║  ██╗    ██████╔╝███████╗██║███████║██║██║  ██║╚█████╔╝
 ╚════╝ ╚═╝  ╚═╝╚═╝  ╚═╝    ╚═════╝ ╚══════╝╚═╝╚══════╝╚═╝╚═╝  ╚═╝ ╚════╝
```

<div align="center">

**Pikselowa strona pogodowa. Zero zależności. Zero kolorów. Tylko dane.**

[![HTML](https://img.shields.io/badge/HTML-single%20file-000000?style=flat-square&logo=html5&logoColor=white)](.)
[![API](https://img.shields.io/badge/API-Open--Meteo-000000?style=flat-square)](https://open-meteo.com)
[![License](https://img.shields.io/badge/license-MIT-000000?style=flat-square)](LICENSE)
[![No deps](https://img.shields.io/badge/dependencies-0-000000?style=flat-square)](.)
[![Website](https://img.shields.io/badge/website-jakdzisiaj.pl-000000?style=flat-square)](https://jakdzisiaj.pl)

</div>

---

## Co to jest

**[jakdzisiaj.pl](https://jakdzisiaj.pl)** to minimalistyczna strona pogodowa utrzymana w estetyce retro pixel-art. Jeden plik HTML, zero frameworków, zero kluczy API.

Inspirowana czarno-białymi aplikacjami terminalowymi i grami z lat 80. Zamiast kolorowych kart i gradientów — czyste dane na czarnym tle, pixelowa czcionka i ręcznie rysowane ikonki SVG.

```
21:37:42

WITAJ W
WARSZAWA
52.2297 N  21.0122 E

☁  12°C
ODCZUWALNA 9°C

POGODA JEST
↑ CIEPLEJ NIZ WCZORAJ (+3C)
CZ. ZACHMURZENIE

WIATR      MAKS     MIN
5 KM/H     13°C     5°C
```

---

## Funkcje

- 📍 **Automatyczna lokalizacja** — geolokalizacja GPS przeglądarki
- 🌡️ **Aktualna pogoda** — temperatura, odczuwalna, wiatr, min/max dnia
- 📅 **Pogoda na cały dzień** — rano / południe / wieczór / noc z prędkością wiatru
- 📆 **Prognoza 10-dniowa** — z pikselowym paskiem zakresu temperatur
- 🔺 **Porównanie z wczoraj** — cieplej / chłodniej / podobnie z pixelową strzałką
- 🎨 **Pixel art ikonki** — ręcznie rysowane 8×8px w SVG (słońce, chmura, deszcz, śnieg, burza, mgła, księżyc)
- 🕐 **Zegar na żywo** — aktualizowany co sekundę
- ☰ **Hamburger menu** — panel boczny z wyszukiwarką dowolnej miejscowości
- 🏙️ **Lista 45 miast** — alfabetyczna lista polskich miast jako fallback gdy brak GPS
- 🔍 **Wyszukiwarka** — Nominatim API, szuka po całej Polsce
- 📱 **Responsive** — mobile, tablet, desktop, duże monitory

---

## Flow lokalizacji

```
Wejście na stronę
       │
       ▼
 Sprawdź uprawnienia GPS
       │
  ┌────┴────┐
  │         │
granted   denied / prompt
  │         │
  ▼         ▼
Pobierz   Zapytaj przeglądarkę
  GPS          │
  │       ┌───┴───┐
  │     OK        BLAD
  │      │          │
  ▼      ▼          ▼
Pogoda  Pogoda   Ekran błędu
                    │
              ┌─────┴──────┐
              │             │
         Spróbuj GPS    Znajdź ręcznie
                            │
                     ┌──────┴──────┐
                     │             │
               Lista 45 miast  Wyszukiwarka
```

---

## Jak uruchomić

```bash
git clone https://github.com/twoj-nick/jakdzisiaj.pl
cd jakdzisiaj.pl
open pogoda.html
```

Lub odwiedź: **[jakdzisiaj.pl](https://jakdzisiaj.pl)**

> Geolokalizacja wymaga HTTPS lub `localhost`. Na `jakdzisiaj.pl` działa natywnie.

---

## Stack

| Warstwa | Technologia |
|---|---|
| Markup | HTML5 |
| Styl | CSS vanilla — `clamp()`, flexbox, `@media` |
| Skrypt | JavaScript ES2020 — bez bundlera |
| Czcionka | [Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P) — Google Fonts |
| Pogoda | [Open-Meteo API](https://open-meteo.com) — darmowe, bez klucza |
| Geokodowanie | [Nominatim / OpenStreetMap](https://nominatim.org) — darmowe |
| Ikonki | Własne pixel-art SVG (siatka 8×8px) |
| Hosting | [jakdzisiaj.pl](https://jakdzisiaj.pl) |

---

## Struktura pliku

```
pogoda.html
│
├── <style>
│   ├── Hamburger + panel boczny
│   ├── Ekran błędu lokalizacji
│   ├── Ekran wyboru miasta (lista + wyszukiwarka)
│   ├── Layout pogody (3 kolumny)
│   └── Responsive breakpoints (700px / 1024px / 1600px)
│
├── <body>
│   ├── .ham-btn            — przycisk hamburger (fixed, z-index 1100)
│   ├── .panel-overlay      — ciemne tło panelu (z-index 1040)
│   ├── .side-panel         — panel boczny z wyszukiwarką (z-index 1050)
│   └── #app                — punkt montowania całej aplikacji
│
└── <script>
    ├── pxIcon()            — renderer pixel-art (piksele → SVG rect)
    ├── ICONS{}             — definicje ikon: sun, cloud, rain, snow...
    ├── wmoIcon()           — kod WMO → ikona SVG
    ├── wmoDesc()           — kod WMO → opis po polsku
    ├── CITIES[]            — lista 45 polskich miast z koordynatami
    ├── getCityName()       — Nominatim reverse geocoding
    ├── fetchWeather()      — Open-Meteo API
    ├── loadWeather()       — orchestrator: fetch → render
    ├── renderWeather()     — buduje cały DOM pogody
    ├── showDenied()        — ekran błędu GPS z instrukcją
    ├── showCityPicker()    — lista alfabetyczna + wyszukiwarka
    ├── openPanel()         — otwiera panel boczny
    ├── doPanelSearch()     — wyszukiwanie w panelu przez Nominatim
    └── init()              — sprawdza permissions → tryGPS()
```

---

## API

### Open-Meteo

```
GET https://api.open-meteo.com/v1/forecast
  ?latitude={lat}
  &longitude={lon}
  &hourly=temperature_2m,weathercode,windspeed_10m,apparent_temperature
  &daily=weathercode,temperature_2m_max,temperature_2m_min
  &timezone=auto
  &past_days=1        ← do porównania z wczoraj
  &forecast_days=11
```

### Nominatim — reverse geocoding

```
GET https://nominatim.openstreetmap.org/reverse
  ?lat={lat}&lon={lon}&format=json&accept-language=pl
```

### Nominatim — wyszukiwanie

```
GET https://nominatim.openstreetmap.org/search
  ?q={query}&countrycodes=pl&format=json&limit=8&accept-language=pl
```

---

## Ikonki pixel-art

Każda ikona to tablica `[col, row, brightness]` na siatce 8×8. Brightness: `2` = biały, `1` = szary, `0` = ciemny.

```js
const SUN = [
  [3,0,1],[4,0,1],           // promienie
  [2,2,2],[3,2,2],[4,2,2],   // tarcza
  // ...
];
pxIcon(SUN, 48); // → SVG 48×48px
```

Dostępne: `sun` · `cloud` · `partly` · `rain` · `snow` · `thunder` · `fog` · `moon` · `arrUp` · `arrDn` · `arrEq`

---

## Changelog

### v1.4.0 — kwiecień 2025
- Wyrzucona mapa Polski — zastąpiona listą alfabetyczną 45 miast
- Naprawiony bug hamburger menu (z-index conflict)
- Panel boczny z wyszukiwarką dostępny zawsze (nie tylko przy braku GPS)
- Wyszukiwarka w dwóch miejscach: panel boczny + ekran wyboru miasta

### v1.3.0 — kwiecień 2025
- Hamburger menu w lewym górnym rogu
- Wysuwany panel boczny z wyszukiwarką miejscowości
- Pikselowa mapa Polski z zaznaczonymi miastami (zastąpiona w v1.4.0)

### v1.2.0 — kwiecień 2025
- Przepisanie na czysty czarno-biały design
- Ikonki SVG pixel-art zastąpiły emoji
- Pełny responsive: mobile / tablet / desktop / 1600px+
- Ekran błędu GPS z instrukcją odblokowania + lista miast

### v1.1.0 — kwiecień 2025
- Geolokalizacja z obsługą błędów i ekranem wyboru miasta
- 3-kolumnowy layout: miasto / pogoda dzienna / prognoza 10 dni
- Prędkość wiatru w każdej porze dnia

### v1.0.0 — kwiecień 2025
- Pierwsza wersja
- Open-Meteo API + Nominatim
- Press Start 2P pixel font
- Prognoza 10-dniowa z paskami temperatur

---

## Licencja

MIT — rób co chcesz, zostaw gwiazdkę jeśli podoba ci się projekt.

---

<div align="center">
<sub>→ <a href="https://jakdzisiaj.pl">jakdzisiaj.pl</a> · zbudowane bez kolorów · bez frameworków · bez sensu</sub>
</div>
