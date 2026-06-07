# Changelog

## [2.1.0] - 2026-06-07

### Added
- **International Friendlies** (`fifa.friendly`) — ESPN scoreboard endpoint, sport detection keywords, and common query mapping for men's international friendly matches. Tested live against Morocco vs Norway (June 7, 2026).

### Changed
- Updated Soccer section of API Endpoints table to include `fifa.friendly` scoreboard URL.
- Updated Sport Detection table with keywords: "international friendly", "friendlies", "friendly match", and national team names (e.g., Morocco, Norway, national team friendly).
- Updated Common Queries table with friendlies routing.

## [2.0.1] - 2026-06-04

### Fixed
- Clarified that The Odds API has zero motorsport coverage (no F1, IndyCar, NASCAR, MotoGP).
- Added "Test before push" pitfall: verify new data sources against live APIs before committing.

## [2.0.0] - 2026-06-02

### Added
- Betting odds support via The Odds API (h2h, spreads, totals).
- API key management (`.env` file, 500 req/month free tier).
- Sport detection keywords for odds queries.
- Common queries for odds lookup.
- Active sports check endpoint.

## [1.0.0] - 2026-05-27

### Added
- Initial release: live scores, standings, and F1 data from ESPN and Ergast APIs.
- Supported leagues: NBA, NFL, MLB, NHL, WNBA, La Liga, Premier League, Champions League, MLS, Bundesliga, Serie A, Ligue 1, Liga MX, Copa Libertadores, FIFA World Cup, F1, UFC/MMA, Tennis, Golf, Rugby.