# hermes-sports-skill

A [Hermes-Agent](https://github.com/NousResearch/hermes-agent) skill for live sports scores, standings, odds, and results. Free APIs for scores/standings; The Odds API (key required) for betting lines.

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

Create `.env` for odds support (optional):

```bash
echo "ODDS_API_KEY=your_key_here" > ~/.hermes/skills/tools/sports-scores/.env
```

Get a free API key at [the-odds-api.com](https://the-odds-api.com/) (500 requests/month free tier).

Restart Hermes or reload skills — the skill activates automatically when sports questions are detected.

## Usage Examples

- "What's the Knicks score?" → fetches NBA scoreboard, finds the Knicks game
- "F1 driver standings" → fetches current F1 driver championship table
- "Where is Barça in La Liga?" → fetches La Liga standings, highlights Barcelona's position
- "World Cup 2026 scores" → fetches FIFA World Cup scoreboard
- "Premier League table" → fetches EPL standings
- "UFC fight card tonight" → fetches UFC event schedule
- "Bundesliga standings" → fetches German league table
- "Barcelona odds" → fetches La Liga h2h odds (falls back to Copa Libertadores if off-season)
- "NBA odds" → fetches NBA moneyline from FanDuel, DraftKings, etc.
- "NFL spreads" → fetches NFL point spreads from US bookmakers
- "MLB over/under" → fetches MLB totals from US bookmakers

## Data Sources

- **ESPN Scoreboard & Standings API** — scores, schedules, and standings for all supported sports (unofficial, no key required)
- **Ergast F1 API** — historical and current F1 results, driver/constructor standings (no key required)
- **OpenF1 API** — live F1 timing data during race sessions (no key required)
- **The Odds API** — betting odds (h2h, spreads, totals) across 164+ sports and 30+ bookmakers (API key required, free tier: 500 req/month)

## Disclaimer

ESPN endpoints are unofficial and may change without notice. This skill uses publicly accessible APIs that are not officially documented for third-party use. Rate limits, response formats, or endpoint URLs may change at any time. Ergast API limits to 4 requests/second. The Odds API is a third-party service — usage is subject to their terms and rate limits. Odds data is for informational purposes only.

## License

MIT — Copyright NovaAI

---

Built by [NovaAI](https://github.com/Drknght4)