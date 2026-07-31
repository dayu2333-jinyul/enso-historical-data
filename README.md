# ENSO Historical Dataset (1950–2026)

[![DOI](https://zenodo.org/badge/DOI/21717522.svg)](https://doi.org/10.5281/zenodo.21717522)
[![npm](https://img.shields.io/npm/v/enso-historical-data)](https://www.npmjs.com/package/enso-historical-data)

> Comprehensive monthly El Niño Southern Oscillation (ENSO) data — 126 months across 8 major El Niño/La Niña events, with ONI values, SOI, and subsurface temperature anomalies.

This dataset provides monthly-resolution Oceanic Niño Index (ONI), Southern Oscillation Index (SOI), and subsurface temperature anomaly data for every significant ENSO event since 1950, including the 2023–24 Super El Niño and emerging 2026 conditions.

## Files

| File | Format | Records | Description |
|------|--------|---------|-------------|
| [`data.csv`](data.csv) | CSV | 126 | Full monthly dataset with all fields |
| [`enso-data.json`](enso-data.json) | JSON | 126 | Machine-readable format for analysis |

## Fields

| Field | Description | Units |
|-------|-------------|-------|
| `Year` | Observation year | — |
| `Month` | Month number (1–12) | — |
| `Nino12` | Niño 1+2 region SST | °C |
| `Nino3` | Niño 3 region SST | °C |
| `Nino34` | Niño 3.4 region SST (standard ONI region) | °C |
| `Nino4` | Niño 4 region SST | °C |
| `ONI` | Oceanic Niño Index (3-month running mean of Niño 3.4 anomaly) | °C |
| `Condition` | ENSO phase classification | Neutral / El_Nino / Super_El_Nino / La_Nina |
| `SOI` | Southern Oscillation Index (Tahiti−Darwin pressure) | hPa |
| `Subsurface_Anomaly` | Equatorial subsurface temperature anomaly (0–300m) | °C |

## ENSO Classification

| Condition | ONI Threshold |
|-----------|---------------|
| Super El Niño | ONI ≥ +2.0°C |
| El Niño | ONI ≥ +0.5°C |
| Neutral | −0.5°C < ONI < +0.5°C |
| La Niña | ONI ≤ −0.5°C |

## Major Events Covered

| Event | Peak Month | Peak ONI | Category |
|-------|------------|----------|----------|
| 1957–58 | Dec 1957 | +1.6°C | El Niño |
| 1965–66 | Jun 1965 | +1.7°C | El Niño |
| 1972–73 | Jul 1972 | +2.1°C | Super |
| 1982–83 | Aug 1982 | +2.4°C | Super |
| 1997–98 | Sep 1997 | +2.5°C | Super |
| 2015–16 | Aug 2015 | +2.6°C | Super |
| 2023–24 | Oct 2023 | +2.1°C | Super |
| 2026–27 | — | — | Developing |

## Quick Start

```python
import csv
with open('data.csv') as f:
    rows = list(csv.DictReader(f))
    supers = [r for r in rows if r['Condition'] == 'Super_El_Nino']
    print(f'{len(supers)} Super El Niño months')
```

```javascript
const data = await fetch('enso-data.json').then(r => r.json());
const oni2023 = data.filter(d => d.Year === '2023');
const avg = oni2023.reduce((s, d) => s + +d.ONI, 0) / oni2023.length;
console.log(`2023 avg ONI: ${avg.toFixed(1)}°C`);
```

## Live Tracker

**[elninoguide.com/dashboard](https://elninoguide.com/dashboard)** — Real-time ENSO data updated daily from NOAA CPC and ECMWF.

## Sources

NOAA CPC, BOM, ECMWF, IRI/Columbia University.

## License

CC0 1.0 Universal — Public Domain.
