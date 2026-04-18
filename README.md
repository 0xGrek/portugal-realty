# Portugal Realty

> Real estate aggregator scraping 4 Portuguese portals — 12K+ listings, fraud detection, 2026 IMT tax rules.

<div align="left">

![Python](https://img.shields.io/badge/Python-1a1a1a?style=flat-square&logo=python&logoColor=cccccc)
![Flask](https://img.shields.io/badge/Flask-1a1a1a?style=flat-square&logo=flask&logoColor=cccccc)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-1a1a1a?style=flat-square&logo=postgresql&logoColor=cccccc)
![httpx](https://img.shields.io/badge/httpx-1a1a1a?style=flat-square&logoColor=cccccc)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-1a1a1a?style=flat-square&logoColor=cccccc)
![Docker](https://img.shields.io/badge/Docker-1a1a1a?style=flat-square&logo=docker&logoColor=cccccc)

</div>

---

## Overview

Built to solve a real problem: finding housing in Portugal as a foreigner means sifting through four fragmented portals with duplicate listings, fraudulent relists, and opaque pricing. Portugal Realty aggregates all four, deduplicates by coordinates, flags suspicious patterns, and adds a financial calculator with current Portuguese tax law.

Built for personal use — now covers 12,000+ active listings across the country.

---

## Architecture

```
ScraperOrchestrator
├── Portal Scrapers (4)
│   ├── IdealistaSpider    — asyncio + httpx, JS-rendered fallback
│   ├── ImovirtualSpider   — paginated async crawl
│   ├── ERA_Spider         — REST API wrapper
│   └── Remax_Spider       — HTML parser + session rotation
├── DeduplicationEngine
│   ├── HaversineFilter    — coordinate-based proximity dedup (50m threshold)
│   ├── PriceNormalizer    — price-per-m² normalization
│   └── FraudDetector      — relisting pattern analysis (554 confirmed)
├── FinancialCalculator
│   ├── IMT_Calculator     — 2026 Portuguese transfer tax rules
│   ├── MortgageModel      — Euribor-linked rate simulation
│   └── RentalYieldCalc    — gross/net yield estimation
├── Flask API              — REST endpoints for frontend
└── PostgreSQL             — listings, price history, fraud flags
```

---

## Key Features

- **4 portal scrapers** — Idealista, Imovirtual, ERA, Remax
- **Coordinate deduplication** — Haversine-based, 50m threshold to catch same-property relists
- **Fraud detection** — 554 fraudulent relisting patterns identified and flagged
- **2026 IMT calculator** — accurate Portuguese transfer tax computation
- **Mortgage simulator** — Euribor-indexed rate scenarios
- **Price history** — track listing price changes over time per property
- **REST API** — clean endpoints for any frontend or analysis layer

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.11+ |
| HTTP | httpx (async), requests |
| Web framework | Flask |
| ORM | SQLAlchemy |
| Database | PostgreSQL |
| Geo math | Haversine formula (custom) |
| Infrastructure | Docker, cron scheduling |

---

## Metrics

- **12,000+** active listings indexed
- **4** portals scraped
- **554** fraudulent relisting patterns detected
- Price history tracked since 2025
- Supports all Portuguese municipalities

---

Live demo: [portugal-realty-server.onrender.com](https://portugal-realty-server.onrender.com/) · Portfolio: [0xgrek.com](https://0xgrek.com)

---

© 2024-2026 Serhii Ivanenko.

Licensed under the [MIT License](LICENSE).
