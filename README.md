# hermes-sports-skill

A [Hermes-Agent](https://github.com/NousResearch/hermes-agent) skill for live sports scores, standings, and results from free public APIs. No API keys required.

## Sports Covered

**US Leagues:** NBA, NFL, MLB, NHL, WNBA

**Soccer:** La Liga, Premier League, Champions League, MLS, Bundesliga, Serie A, Ligue 1, Liga MX, Copa Libertadores, FIFA World Cup

**Motorsport:** Formula 1 (Ergast + OpenF1)

**Other:** UFC/MMA, Tennis (ATP/WTA), Golf (PGA), Rugby

## Installation

Copy the skill file to your Hermes skills directory:

```bash
mkdir -p ~/.hermes/skills/tools/sports-scores
cp SKILL.md ~/.hermes/skills/tools/sports-scores/SKILL.md
```

Restart Hermes or reload skills — the skill activates automatically when sports questions are detected.

## Usage Examples

- "What's the Knicks score?" → fetches NBA scoreboard, finds the Knicks game
- "F1 driver standings" → fetches current F1 driver championship table
- "Where is Barça in La Liga?" → fetches La Liga standings, highlights Barcelona's position
- "World Cup 2026 scores" → fetches FIFA World Cup scoreboard
- "Premier League table" → fetches EPL standings
- "UFC fight card tonight" → fetches UFC event schedule
- "Bundesliga standings" → fetches German league table

## Data Sources

- **ESPN Scoreboard & Standings API** — scores, schedules, and standings for all supported sports (unofficial, no key required)
- **Ergast F1 API** — historical and current F1 results, driver/constructor standings (no key required)
- **OpenF1 API** — live F1 timing data during race sessions (no key required)

## Disclaimer

ESPN endpoints are unofficial and may change without notice. This skill uses publicly accessible APIs that are not officially documented for third-party use. Rate limits, response formats, or endpoint URLs may change at any time. Ergast API limits to 4 requests/second.

## License

MIT — Copyright NovaAI

---

Built by [NovaAI](https://github.com/Drknght4)