# Sun Path Tracker

An interactive visualisation of the sun's path across the sky for any day, at any of five preset cities. Computes sunrise, sunset, max elevation and the live azimuth/altitude using standard astronomical formulas, then animates the sun along its arc.

**Live demo:** https://tatutomp.github.io/sun_tracker/

## Features

- **Seven city presets** with correct latitudes and IANA time zones:
  - Helsinki (60.17°N, Europe/Helsinki)
  - Kotka (60.47°N, Europe/Helsinki)
  - Siikajoki (64.25°N, Europe/Helsinki)
  - Narvik (68.44°N, Europe/Oslo) — above the Arctic Circle, so polar day/night kicks in
  - Las Palmas (28.10°N, Atlantic/Canary)
  - Shanghai (31.23°N, Asia/Shanghai)
  - London (51.51°N, Europe/London)
- **Date navigation** — step a day at a time or jump to today.
- **"Now" animation** — sweeps the sun from sunrise up to the current moment, showing where it is *right now* in the selected city.
- **Live readouts** — sunrise, solar noon, sunset, current elevation, current azimuth (with cardinal direction), max elevation of the day, day length, latitude and current time.
- **Hand-drawn scene** — sky gradient, procedural starfield, dashed sun arc with hour-tick dots, horizon line, Helsinki-style skyline silhouette, ground gradient, glowing sun whose colour warms toward sunrise/sunset.
- **No build step, no dependencies.** A single `index.html` (~22 KB) with inline CSS and vanilla JS. Works offline once loaded.

## How it works

Solar geometry uses the simplified formulas commonly cited for everyday sun-position calculations:

- **Declination** — `δ = −23.44° · cos((360°/365) · (N + 10))` where `N` is the day of the year.
- **Sunrise/sunset hour angle** — `cos H = −tan(φ) · tan(δ)` where `φ` is the latitude. The two roots give sunrise (`12 − H/15`) and sunset (`12 + H/15`) in solar hours.
- **Max elevation** — `90° − |φ − δ|`.
- **Instantaneous altitude/azimuth** — derived from the local hour angle, latitude and declination via the standard horizontal-coordinate transform.

Time-zone handling uses `Intl.DateTimeFormat` to read the current hour, minute and date directly in the city's IANA zone, so DST transitions are handled by the browser rather than ad-hoc offsets.

## Run locally

```
open index.html
```

Or just double-click the file. There is nothing to install.

## Origin

Ported from a SwiftUI iOS app (`SunTracker/ContentView.swift`), which was itself a port of a HarmonyOS ArkTS version. The math and visual design are 1:1 with the SwiftUI source — only the rendering primitives differ (HTML canvas instead of SwiftUI `Canvas`).
