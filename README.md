```
██████╗  ██████╗  ██████╗  ██████╗ ██████╗  █████╗
██╔══██╗██╔═══██╗██╔════╝ ██╔═══██╗██╔══██╗██╔══██╗
██████╔╝██║   ██║██║  ███╗██║   ██║██║  ██║███████║
██╔═══╝ ██║   ██║██║   ██║██║   ██║██║  ██║██╔══██║
██║     ╚██████╔╝╚██████╔╝╚██████╔╝██████╔╝██║  ██║
╚═╝      ╚═════╝  ╚═════╝  ╚═════╝ ╚═════╝ ╚═╝  ╚═╝
```

<div align="center">

**Pikselowa strona pogodowa. Zero zależności. Zero kolorów. Tylko dane.**

[![HTML](https://img.shields.io/badge/HTML-single%20file-000000?style=flat-square&logo=html5&logoColor=white)](.)
[![API](https://img.shields.io/badge/API-Open--Meteo-000000?style=flat-square)](https://open-meteo.com)
[![License](https://img.shields.io/badge/license-MIT-000000?style=flat-square)](LICENSE)
[![No deps](https://img.shields.io/badge/dependencies-0-000000?style=flat-square)](.)

</div>

---

## Co to jest

**POGODA** to minimalistyczna strona pogodowa utrzymana w estetyce retro pixel-art. Jeden plik HTML, zero frameworków, zero kluczy API. Otwierasz w przeglądarce — działa.

Inspirowana czarno-białymi aplikacjami terminalowymi i grami z lat 80. Zamiast kolorowych kart i gradientów — czyste dane na czarnym tle, pixelowa czcionka i ręcznie rysowane ikonki SVG.

```
00:00:00
WITAJ W
WROCŁAW
51.1079 N  17.0385 E

☁  12°C
ODCZUWALNA 9°C

POGODA JEST
↑ CIEPLEJ NIZ WCZORAJ (+3C)
CZ. ZACHMURZENIE
```

---

## Funkcje

- 📍 **Automatyczna lokalizacja** — geolokalizacja przeglądarki, fallback na Wrocław
- 🌡️ **Aktualna pogoda** — temperatura, odczuwalna, wiatr, min/max
- 📅 **Pogoda na cały dzień** — rano / południe / wieczór / noc
- 📆 **Prognoza 10-dniowa** — z paskami zakresu temperatur
- 🔺 **Porównanie z wczoraj** — cieplej / chłodniej / podobnie
- 🎨 **Pixel art ikonki** — ręcznie rysowane jako siatka 8×8 px w SVG
- 🕐 **Zegar na żywo** — aktualizowany co sekundę
- 🌐 **Odwrotne geokodowanie** — współrzędne → nazwa miasta po polsku

---

## Jak uruchomić

```bash
# Sklonuj repozytorium
git clone https://github.com/twoj-nick/pogoda
cd pogoda

# Otwórz w przeglądarce
open pogoda.html
# lub po prostu przeciągnij plik do okna przeglądarki
```

> **Uwaga:** Geolokalizacja wymaga kontekstu HTTPS lub `localhost`. Na lokalnym pliku `file://` przeglądarka może zapytać o zgodę lub użyć fallbacku.

Brak serwera. Brak Node.js. Brak npm. Jeden plik.

---

## Stack

| Warstwa | Technologia |
|---|---|
| Markup | HTML5 |
| Styl | CSS (vanilla, bez frameworka) |
| Skrypt | JavaScript (ES2020, bez bundlera) |
| Czcionka | [Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P) — Google Fonts |
| Pogoda | [Open-Meteo API](https://open-meteo.com) — darmowe, bez klucza |
| Geokodowanie | [Nominatim / OpenStreetMap](https://nominatim.org) — darmowe |
| Ikonki | Własne pixel-art SVG (8×8 grid) |

---

## Struktura pliku

```
pogoda.html
│
├── <style>          CSS — layout, typografia, scanlines
├── <body>           Jeden div #app jako punkt montowania
└── <script>
    ├── pxIcon()     Renderer ikon pixel-art (piksele → SVG)
    ├── ICONS{}      Definicje ikon: słońce, chmura, deszcz, śnieg...
    ├── wmoIcon()    Mapowanie kodu WMO → ikona
    ├── wmoDesc()    Mapowanie kodu WMO → opis po polsku
    ├── getCityName() Nominatim reverse geocoding
    ├── fetchWeather() Open-Meteo API call
    ├── render()     Buduje cały DOM z danych pogodowych
    └── main()       Geolokalizacja → fetch → render
```

---

## API

### Open-Meteo

Dane pobierane jednym requestem GET, bez autoryzacji:

```
GET https://api.open-meteo.com/v1/forecast
  ?latitude={lat}
  &longitude={lon}
  &hourly=temperature_2m,weathercode,windspeed_10m,apparent_temperature
  &daily=weathercode,temperature_2m_max,temperature_2m_min
  &timezone=auto
  &past_days=1
  &forecast_days=11
```

`past_days=1` służy do porównania dzisiejszej pogody z wczorajszą.

### Nominatim

```
GET https://nominatim.openstreetmap.org/reverse
  ?lat={lat}
  &lon={lon}
  &format=json
  &accept-language=pl
```

---

## Ikonki pogodowe

Każda ikona to tablica pikseli na siatce 8×8. Każdy piksel to `[col, row, brightness]` gdzie brightness: `2` = biały, `1` = szary, `0` = ciemny szary.

```js
const SUN = [
  [3,0,1],[4,0,1],          // promień górny
  [2,2,2],[3,2,2],[4,2,2],  // tarcza
  // ...
];

pxIcon(SUN, 44); // renderuje jako SVG 44×44px
```

Dostępne ikony: `sun` · `cloud` · `partly` · `rain` · `snow` · `thunder` · `fog` · `moon` · `arrUp` · `arrDn` · `arrEq`

---

## Changelog

### v1.2.0 — 2025-04
- Przepisanie na czysty czarno-biały design
- Usunięcie wszystkich kolorów (nie ma już zielonego LED, pomarańczowych strzałek)
- Uproszczenie layoutu — zero paneli, zero ramek
- Ikonki SVG pixel-art zastąpiły emoji

### v1.1.0 — 2025-04
- Dodanie efektu scanlines (CRT)
- Pixel kursor
- Zielony LED w topbarze
- Kolorowe strzałki dla porównania temperatury

### v1.0.0 — 2025-04
- Pierwsza wersja
- Geolokalizacja + Open-Meteo
- Prognoza 10-dniowa
- Czcionka Press Start 2P
- Podział na rano / południe / wieczór / noc

---

## Licencja

MIT — rób co chcesz, zostaw gwiazdkę jeśli podoba ci się projekt.

---

<div align="center">
<sub>zbudowane bez kolorów · bez frameworków · bez sensu</sub>
</div>
