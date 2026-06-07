---
name: sports-scores
description: Live scores, standings, odds, and F1 data from ESPN, Ergast, and The Odds API.
version: 2.1.0
author: Cipher
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [sports, scores, nba, nfl, mlb, nhl, soccer, f1, espn, live, standings, odds, betting]
    category: tools
    requires_toolsets: [terminal]
    favorite_teams:
      soccer:
        - FC Barcelona (La Liga)
      f1:
        - All drivers — no single team bias
---

# Sports Scores

Live scores, standings, odds, and F1 data from free public APIs plus The Odds API for betting lines.

## API Keys

| API | Required | Location |
|-----|----------|----------|
| ESPN | No | — |
| Ergast / OpenF1 | No | — |
| The Odds API | Yes — for odds queries | `~/.hermes/skills/tools/sports-scores/.env` → `ODDS_API_KEY` |

If `ODDS_API_KEY` is missing, odds commands will fail gracefully with a message to configure the key. Scores and standings work without it.

## Installation

```bash
# From GitHub repo (recommended)
hermes skills install https://github.com/Drknght4/hermes-sports-skill

# Or manually
cp SKILL.md ~/.hermes/skills/tools/sports-scores/SKILL.md
```

Repo: [github.com/Drknght4/hermes-sports-skill](https://github.com/Drknght4/hermes-sports-skill)

Restart Hermes or reload skills — the skill activates automatically when sports questions are detected.

## When to Use

- User asks about any sports score, game result, or standings
- User asks "how did [team] do" or "what's the score"
- User asks about F1 race results, driver standings, or next race
- User asks about betting odds, lines, spreads, or over/unders
- User says "odds on", "what are the odds", "betting line", "Vegas line", "spread"
- User says team name, sport name, or league name casually ("Knicks game", "F1 standings", "Premier League table")

## API Endpoints

### ESPN (no key required)

| Sport | League | Scores | Standings |
|-------|--------|--------|-----------|
| Basketball | NBA | `https://site.api.espn.com/apis/site/v2/sports/basketball/nba/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/basketball/nba/standings` |
| Football | NFL | `https://site.api.espn.com/apis/site/v2/sports/football/nfl/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/football/nfl/standings` |
| Baseball | MLB | `https://site.api.espn.com/apis/site/v2/sports/baseball/mlb/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/baseball/mlb/standings` |
| Hockey | NHL | `https://site.api.espn.com/apis/site/v2/sports/hockey/nhl/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/hockey/nhl/standings` |
| Soccer | La Liga | `https://site.api.espn.com/apis/site/v2/sports/soccer/esp.1/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/esp.1/standings` |
| Soccer | Premier League | `https://site.api.espn.com/apis/site/v2/sports/soccer/eng.1/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/eng.1/standings` |
| Soccer | Champions League | `https://site.api.espn.com/apis/site/v2/sports/soccer/UEFA.CHAMPIONS/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/UEFA.CHAMPIONS/standings` |
| Soccer | MLS | `https://site.api.espn.com/apis/site/v2/sports/soccer/usa.1/scoreboard` | — |
| Soccer | Bundesliga | `https://site.api.espn.com/apis/site/v2/sports/soccer/ger.1/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/ger.1/standings` |
| Soccer | Serie A | `https://site.api.espn.com/apis/site/v2/sports/soccer/ita.1/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/ita.1/standings` |
| Soccer | Ligue 1 | `https://site.api.espn.com/apis/site/v2/sports/soccer/fra.1/scoreboard` | `https://site.api.espn.com/apis/site/v2/sports/soccer/fra.1/standings` |
| Soccer | Liga MX | `https://site.api.espn.com/apis/site/v2/sports/soccer/mex.1/scoreboard` | — |
| Soccer | Copa Libertadores | `https://site.api.espn.com/apis/site/v2/sports/soccer/CONMEBOL.LIBERTADORES/scoreboard` | — |
| Soccer | FIFA World Cup | `https://site.api.espn.com/apis/site/v2/sports/soccer/fifa.world/scoreboard` | — |
| Soccer | International Friendlies | `https://site.api.espn.com/apis/site/v2/sports/soccer/fifa.friendly/scoreboard` | — |

| MMA/UFC | UFC | `https://site.api.espn.com/apis/site/v2/sports/mma/ufc/scoreboard` | — |
| Tennis | ATP/WTA | `https://site.api.espn.com/apis/site/v2/sports/tennis/scoreboard` | — |
| Golf | PGA | `https://site.api.espn.com/apis/site/v2/sports/golf/pga/scoreboard` | — |
| Rugby | Rugby | `https://site.api.espn.com/apis/site/v2/sports/rugby/scoreboard` | — |
| Basketball | WNBA | `https://site.api.espn.com/apis/site/v2/sports/basketball/wnba/scoreboard` | — |

### Ergast F1 API (no key required)

| Data | Endpoint |
|------|-----------|
| Last race results | `https://ergast.com/api/f1/current/last/results.json` |
| Driver standings | `https://ergast.com/api/f1/current/driverStandings.json` |
| Constructor standings | `https://ergast.com/api/f1/current/constructorStandings.json` |
| Next race | `https://ergast.com/api/f1/current/next.json` |
|| Live timing | `https://api.openf1.org/v1/position?session_key=latest` |

### The Odds API (API key required)

Base URL: `https://api.the-odds-api.com`
Auth: `apiKey` query parameter (stored in `~/.hermes/skills/tools/sports-scores/.env` as `ODDS_API_KEY`)

**Key endpoint:**
```
GET /v4/sports/{sport_key}/odds/?apiKey={KEY}&regions=us,eu&markets=h2h
```

**Parameters:**
- `regions` — `us`, `eu`, `uk`, `au`, or comma-separated (default: `us,eu`)
- `markets` — `h2h` (moneyline), `spreads`, `totals` (over/under), or comma-separated (default: `h2h`)
- `oddsFormat` — `decimal` (default), `american`
- `dateFormat` — `iso` (default)

**Available sports** — fetch the full list with:
```bash
curl -s "https://api.the-odds-api.com/v4/sports/?apiKey=$ODDS_API_KEY"
```

**Common sport keys for odds:**

| Sport | Odds API Key | Notes |
|-------|-------------|-------|
| NFL | `americanfootball_nfl` | Active Sep–Feb |
| NBA | `basketball_nba` | Active Oct–Jun |
| MLB | `baseball_mlb` | Active Mar–Oct |
| NHL | `icehocey_nhl` | Active Oct–Jun |
| La Liga | `soccer_spain_la_liga` | In-season only (`active=true`) |
| Premier League | `soccer_epl` | In-season only |
| Champions League | `soccer_uefa_champs_league` | In-season only |
| MLS | `soccer_usa_mls` | In-season only |
| Bundesliga | `soccer_germany_bundesliga` | In-season only |
| Serie A | `soccer_italy_serie_a` | In-season only |
| Ligue 1 | `soccer_france_ligue_one` | In-season only |
| Copa Libertadores | `soccer_conmebol_copa_libertadores` | Year-round |
| FIFA World Cup | `soccer_fifa_world_cup` | Tournament only |
| WNBA | `basketball_wnba` | Active May–Oct |
| UFC/MMA | `mma_mixed_martial_arts` | Event-based |

**Seasonality:** Many sports return empty results (`[]`) when out of season. Always check the `/v4/sports/` endpoint — the `active` field shows whether a sport currently has odds available.

## Sport Detection

Map the user's question to the right endpoint:

|| Keywords | Sport | League Code | Odds API Key |
||----------|-------|-------------|-------------|
|| nba, basketball, knicks, lakers, celtics, warriors, bucks, etc. | Basketball | nba | `basketball_nba` |
|| nfl, football, superbowl, chiefs, 49ers, cowboys, patriots, etc. | Football | nfl | `americanfootball_nfl` |
|| mlb, baseball, yankees, dodgers, mets, red sox, etc. | Baseball | mlb | `baseball_mlb` |
|| nhl, hockey, rangers, avalanche, panthers, oilers, etc. | Hockey | nhl | `icehocey_nhl` |
|| la liga, barcelona, barca, real madrid, atletico, spanish league | Soccer | esp.1 | `soccer_spain_la_liga` |
|| premier league, epl, manchester, liverpool, arsenal, chelsea, english league | Soccer | eng.1 | `soccer_epl` |
|| champions league, ucl, champions | Soccer | UEFA.CHAMPIONS | `soccer_uefa_champs_league` |
|| mls, inter miami, lafc, american soccer | Soccer | usa.1 | `soccer_usa_mls` |
|| world cup, fifa, fifa world cup, mundial | Soccer | fifa.world | `soccer_fifa_world_cup` |
|| international friendly, friendlies, friendly match, morocco, norway, national team friendly | Soccer | fifa.friendly | — |
|| bundesliga, bayern, dortmund, german league | Soccer | ger.1 | `soccer_germany_bundesliga` |
|| serie a, ac milan, inter, juve, juventus, italian league | Soccer | ita.1 | `soccer_italy_serie_a` |
|| ligue 1, psg, paris saint-germain, french league | Soccer | fra.1 | `soccer_france_ligue_one` |
|| liga mx, mexican league, club america, chivas | Soccer | mex.1 | — |
|| copa libertadores, libertadores | Soccer | CONMEBOL.LIBERTADORES | `soccer_conmebol_copa_libertadores` |
|| ufc, mma, ufc fight night, octagon | MMA | ufc | `mma_mixed_martial_arts` |
|| tennis, atp, wta, wimbledon, roland garros, us open tennis, australian open | Tennis | tennis | — |
|| golf, pga, masters, pga tour | Golf | pga | — |
|| rugby, rugby world cup, six nations | Rugby | rugby | — |
|| wnba, women's basketball | Basketball | wnba | `basketball_wnba` |
|| f1, formula 1, formula one, grand prix, gp, race, verstappen, hamilton, leclerc, etc. | F1 | f1 | — |

## Fetching Data

Always use `terminal` with `curl` + `python3` for JSON parsing. Example patterns:

### Scores (ESPN)

```bash
curl -s "https://site.api.espn.com/apis/site/v2/sports/basketball/nba/scoreboard" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for ev in d.get('events', []):
    name = ev.get('name', '')
    status = ev.get('status', {}).get('type', {}).get('description', '')
    short_detail = ev.get('status', {}).get('type', {}).get('shortDetail', '')
    for c in ev.get('competitions', []):
        for comp in c.get('competitors', []):
            team = comp.get('team', {}).get('abbreviation', '')
            score = comp.get('score', '?')
            home_away = 'HOME' if comp.get('homeAway') == 'home' else 'AWAY'
            print(f'{home_away} {team}: {score}')
        print(f'  Status: {status} - {short_detail}')
        print()
"
```

### Standings (ESPN — NBA/NFL/MLB/NHL)

```bash
curl -s "https://site.api.espn.com/apis/site/v2/sports/basketball/nba/standings" | python3 -c "
import sys, json
d = json.load(sys.stdin)
# Standings structure varies by sport — parse entries appropriately
# NBA: entries[].teamStats[] with stats like wins, losses, gamesBehind, etc.
for entry in d.get('standings', {}).get('entries', [])[:10]:
    team = entry.get('team', {})
    abbr = team.get('abbreviation', '')
    name = team.get('shortDisplayName', '')
    stats = {}
    for s in entry.get('stats', []):
        stats[s.get('name')] = s.get('value')
    wins = stats.get('wins', '?')
    losses = stats.get('losses', '?')
    pct = stats.get('winPercent', '?')
    gb = stats.get('gamesBehind', '?')
    print(f'{abbr:4} {name:20} {wins}-{losses}  PCT: {pct}  GB: {gb}')
"
```

### Standings (ESPN — Soccer / La Liga / Premier League)

Soccer standings use a different structure — group entries with team stats inside.

```bash
curl -s "https://site.api.espn.com/apis/site/v2/sports/soccer/esp.1/standings" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for entry in d.get('standings', {}).get('entries', []):
    team = entry.get('team', {})
    name = team.get('shortDisplayName', team.get('displayName', ''))
    abbr = team.get('abbreviation', '')
    stats = {}
    for s in entry.get('stats', []):
        stats[s.get('name')] = s.get('value')
    wins = stats.get('wins', '?')
    losses = stats.get('losses', '?')
    draws = stats.get('ties', stats.get('draws', '?'))
    pts = stats.get('points', '?')
    gd = stats.get('goalDiff', stats.get('goalDifference', '?'))
    played = stats.get('gamesPlayed', stats.get('matchesPlayed', '?'))
    pos = stats.get('rank', stats.get('position', '?'))
    print(f'{str(pos):>2}. {name:<24} P{played}  W{wins} D{draws} L{losses}  GD{gd}  Pts:{pts}')
"
```

For Premier League, replace `esp.1` with `eng.1` in the URL. For Champions League, replace `esp.1` with `UEFA.CHAMPIONS`.

### Standings (ESPN — Champions League)

Champions League uses group-stage format. Parse group entries the same way as La Liga.

```bash
curl -s "https://site.api.espn.com/apis/site/v2/sports/soccer/UEFA.CHAMPIONS/standings" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for entry in d.get('standings', {}).get('entries', []):
    team = entry.get('team', {})
    name = team.get('shortDisplayName', team.get('displayName', ''))
    abbr = team.get('abbreviation', '')
    stats = {}
    for s in entry.get('stats', []):
        stats[s.get('name')] = s.get('value')
    wins = stats.get('wins', '?')
    losses = stats.get('losses', '?')
    draws = stats.get('ties', stats.get('draws', '?'))
    pts = stats.get('points', '?')
    gd = stats.get('goalDiff', stats.get('goalDifference', '?'))
    played = stats.get('gamesPlayed', stats.get('matchesPlayed', '?'))
    pos = stats.get('rank', stats.get('position', '?'))
    print(f'{str(pos):>2}. {name:<24} P{played}  W{wins} D{draws} L{losses}  GD{gd}  Pts:{pts}')
"
```

### F1 — Last Race Results

```bash
curl -s "https://ergast.com/api/f1/current/last/results.json" | python3 -c "
import sys, json
d = json.load(sys.stdin)
race = d['MRData']['RaceTable']['Races'][0]
print(f'{race[\"raceName\"]} — {race[\"date\"]}')
print(f'Circuit: {race[\"Circuit\"][\"circuitName\"]}')
print()
for r in race['Results'][:10]:
    pos = r['position']
    driver = f'{r[\"Driver\"][\"givenName\"]} {r[\"Driver\"][\"familyName\"]}'
    constructor = r['Constructor']['name']
    time = r.get('Time', {}).get('time', r.get('status', ''))
    points = r['points']
    print(f'P{pos:>2}: {driver:<24} {constructor:<16} {time}')
"
```

### F1 — Driver Standings

```bash
curl -s "https://ergast.com/api/f1/current/driverStandings.json" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for entry in d['MRData']['StandingsTable']['StandingsLists'][0]['DriverStandings']:
    pos = entry['position']
    driver = f'{entry[\"Driver\"][\"givenName\"]} {entry[\"Driver\"][\"familyName\"]}'
    constructor = entry['Constructors'][0]['name']
    wins = entry['wins']
    points = entry['points']
    print(f'P{pos:>2}: {driver:<22} {constructor:<16} W:{wins:>2} Pts:{points:>4}')
"
```

### F1 — Next Race

```bash
curl -s "https://ergast.com/api/f1/current/next.json" | python3 -c "
import sys, json
d = json.load(sys.stdin)
race = d['MRData']['RaceTable']['Races'][0]
print(f'Next: {race[\"raceName\"]}')
print(f'Date: {race[\"date\"]}')
print(f'Circuit: {race[\"Circuit\"][\"circuitName\"]}')
print(f'Location: {race[\"Circuit\"][\"Location\"][\"locality\"]}, {race[\"Circuit\"][\"Location\"][\"country\"]}')
"
```

### F1 — Live Timing (during race sessions)

```bash
curl -s "https://api.openf1.org/v1/position?session_key=latest" | python3 -c "
import sys, json
d = json.load(sys.stdin)
# Sort by position
positions = sorted(d, key=lambda x: x.get('position', 999))
if not positions:
    print('No live session currently active')
else:
    session = positions[0].get('session_key', 'unknown')
    print(f'Session: {session}')
    for p in positions:
        pos = p.get('position', '?')
        driver = p.get('driver_number', '?')
        print(f'P{pos}: #{driver}')
"
```

### Odds — H2H / Moneyline (The Odds API)

```bash
# Read API key from skill .env
ODDS_API_KEY=$(grep ODDS_API_KEY ~/.hermes/skills/tools/sports-scores/.env | cut -d= -f2)

# Fetch odds for a sport (example: NBA)
curl -s "https://api.the-odds-api.com/v4/sports/basketball_nba/odds/?apiKey=${ODDS_API_KEY}&regions=us,eu&markets=h2h" | python3 -c "
import sys, json
d = json.load(sys.stdin)
if not d:
    print('No upcoming odds found — sport may be off-season.')
for ev in d[:8]:
    home = ev.get('home_team', '?')
    away = ev.get('away_team', '?')
    commence = ev.get('commence_time', '?')[:16]
    print(f'{home} vs {away}  ({commence})')
    for bk in ev.get('bookmakers', [])[:3]:
        for m in bk.get('markets', []):
            if m['key'] == 'h2h':
                prices = ' | '.join([f\"{o['name']}: {o['price']}\" for o in m.get('outcomes', [])])
                print(f'  {bk[\"key\"]}: {prices}')
    print()
"
```

### Odds — Spreads & Totals (The Odds API)

```bash
ODDS_API_KEY=$(grep ODDS_API_KEY ~/.hermes/skills/tools/sports-scores/.env | cut -d= -f2)

# Spreads (point spreads for US sports)
curl -s "https://api.the-odds-api.com/v4/sports/basketball_nba/odds/?apiKey=${ODDS_API_KEY}&regions=us&markets=spreads" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for ev in d[:5]:
    home = ev.get('home_team', '?')
    away = ev.get('away_team', '?')
    print(f'{home} vs {away}')
    for bk in ev.get('bookmakers', [])[:2]:
        for m in bk.get('markets', []):
            if m['key'] == 'spreads':
                lines = ' | '.join([f\"{o['name']}: {o.get('point','?')} ({o['price']})\" for o in m.get('outcomes', [])])
                print(f'  {bk[\"key\"]}: {lines}')
    print()
"

# Totals (over/under)
curl -s "https://api.the-odds-api.com/v4/sports/basketball_nba/odds/?apiKey=${ODDS_API_KEY}&regions=us&markets=totals" | python3 -c "
import sys, json
d = json.load(sys.stdin)
for ev in d[:5]:
    home = ev.get('home_team', '?')
    away = ev.get('away_team', '?')
    print(f'{home} vs {away}')
    for bk in ev.get('bookmakers', [])[:2]:
        for m in bk.get('markets', []):
            if m['key'] == 'totals':
                lines = ' | '.join([f\"{o['name']}: {o.get('point','?')} ({o['price']})\" for o in m.get('outcomes', [])])
                print(f'  {bk[\"key\"]}: {lines}')
    print()
"
```

### Odds — Check Active Sports

```bash
ODDS_API_KEY=$(grep ODDS_API_KEY ~/.hermes/skills/tools/sports-scores/.env | cut -d= -f2)

# List only currently active sports with odds
curl -s "https://api.the-odds-api.com/v4/sports/?apiKey=${ODDS_API_KEY}" | python3 -c "
import sys, json
sports = json.load(sys.stdin)
active = [s for s in sports if s.get('active')]
for s in sorted(active, key=lambda x: x['key']):
    print(f\"{s['key']:<40} {s['title']}\")
print(f'Active: {len(active)} / {len(sports)}')
"
```

### Odds — American Format

Append `&oddsFormat=american` to any odds URL to get American odds (e.g., `-110`, `+150`) instead of decimal (e.g., `1.91`, `2.50`).

```bash
ODDS_API_KEY=$(grep ODDS_API_KEY ~/.hermes/skills/tools/sports-scores/.env | cut -d= -f2)
curl -s "https://api.the-odds-api.com/v4/sports/basketball_nba/odds/?apiKey=${ODDS_API_KEY}&regions=us&markets=h2h&oddsFormat=american"
```

## Output Rules

1. **Clean format.** Never dump raw JSON. Parse and present human-readable summaries.
2. **Live games.** If a game status is "In Progress" or similar, clearly note it: **🔴 LIVE**.
3. **Scheduled games.** Show date, time, and broadcast info.
4. **Completed games.** Show final score with winner bold or marked.
5. **Standings.** Top 10 only unless user asks for full table.
6. **F1.** Show driver name, constructor, position, and points/gap.
7. **User preferences.** FC Barcelona (La Liga) and F1 are the user's favorites. Highlight these when they appear.
8. **Time zones.** Always show times in Eastern Time (EDT/EST). Convert from UTC when needed.
9. **Multiple games.** If asking about a league, show all games for today. If asking about a team, show just that team's game.
10. **Odds require API key.** The Odds API requires `ODDS_API_KEY` in `.env`. If missing, report it — don't skip silently. ESPN and Ergast remain keyless.

## Sport-Specific Notes

### NBA
- Playoff brackets: ESPN doesn't have a clean bracket endpoint. For playoff series, use the scoreboard and look for series summaries.
- Standings use Eastern/Western conference split.

### NFL
- NFL season is Sept–Feb. Off-season queries will return empty scoreboards.
- Standings use AFC/NFC conference split.

### Soccer
- La Liga, Premier League, Champions League, and MLS are the supported leagues.
- Soccer scoreboards show matchday groupings. Parse `competitions[0].competitors` for scores.
- Barcelona is the user's team — always highlight their match when present.

### F1
- Ergast API is reliable but sometimes 1-2 hours behind live.
- For truly live data during a race, use the OpenF1 API.
- Constructor standings show team championship points.
- Driver number plus name is the standard format.

## Common Queries

| User asks | Action |
|-----------|--------|
| "Knicks score" | Fetch NBA scoreboard, find Knicks game, show score |
| "NBA standings" | Fetch NBA standings, show top 10 |
| "MLS" | Fetch usa.1 scoreboard, show all matches |
| "World Cup" or "FIFA" | Fetch fifa.world scoreboard, show all matches |
| "International friendly" or "friendlies" | Fetch fifa.friendly scoreboard, show all matches |
| "Bundesliga" | Fetch ger.1 scoreboard, show all matches |
| "Bundesliga standings" | Fetch ger.1 standings, show full table |
| "Serie A" | Fetch ita.1 scoreboard, show all matches |
| "Serie A standings" | Fetch ita.1 standings, show full table |
| "Ligue 1" | Fetch fra.1 scoreboard, show all matches |
| "Ligue 1 standings" | Fetch fra.1 standings, show full table |
| "Liga MX" | Fetch mex.1 scoreboard, show all matches |
| "Copa Libertadores" | Fetch CONMEBOL.LIBERTADORES scoreboard |
| "UFC" or "MMA" | Fetch UFC scoreboard, show fight card |
| "Tennis" | Fetch tennis scoreboard, show matches |
| "Golf" or "PGA" | Fetch PGA scoreboard, show leaderboard |
| "Rugby" | Fetch rugby scoreboard, show matches |
| "WNBA" | Fetch WNBA scoreboard, show all games |
| "Barcelona" | Fetch esp.1 scoreboard, find Barca match, highlight it |
| "La Liga standings" | Fetch esp.1 standings, show full table |
| "Premier League table" | Fetch eng.1 standings, show full table |
| "Champions League" or "UCL" | Fetch UEFA.CHAMPIONS scoreboard or standings |
| "Champions League standings" | Fetch UEFA.CHAMPIONS standings, show group tables |
| "F1 standings" | Fetch driver standings, show top 10 |
| "F1 results" | Fetch last race results, show top 10 |
| "Who won last night" | Fetch relevant sport's scoreboard, filter completed games |
| "NFL scores" | Fetch NFL scoreboard, show all games |
| "MLB standings" | Fetch MLB standings, show top 10 by division |
|| "Is there a hockey game on" | Fetch NHL scoreboard, show schedule |
| "Barcelona odds" or "Barça odds" | Fetch soccer_spain_la_liga odds, find Barca match. Fall back to Copa Libertadores if La Liga is off-season |
| "NBA odds" | Fetch basketball_nba odds, show h2h from top bookmakers |
| "NFL odds" or "NFL spreads" | Fetch americanfootball_nfl odds with h2h or spreads market |
| "MLB odds" | Fetch baseball_mlb odds, show h2h |
| "What are the odds on [team]" | Detect sport → use Odds API key from sport detection table |

## Pitfalls

- ESPN API responses are large. Use `python3 -c` to parse inline — don't dump full JSON.
- Soccer league codes are not intuitive: `esp.1` (La Liga), `eng.1` (Premier League), `UEFA.CHAMPIONS` (Champions League), `usa.1` (MLS). Always use the exact codes.
- Ergast rate limits to 4 requests/second. If you hit live timing + standings + results in one turn, add a 1-second pause between calls.
- ESPN scoreboard dates default to "today" in US Eastern Time. For historical dates, append `?dates=YYYYMMDD` parameter.
- OpenF1 live timing returns empty when no session is active — that's normal, not an error.
- F1 Ergast API uses `MRData` wrapper — always parse through `['MRData']['RaceTable']` or `['MRData']['StandingsTable']`.
- Bundesliga/Serie A/Ligue 1 standings use the same soccer parsing pattern as La Liga — replace `esp.1` with `ger.1`, `ita.1`, or `fra.1`.
- Liga MX and Copa Libertadores are scoreboard-only (no standings endpoint).
- UFC/MMA scoreboard uses `sports/mma/ufc` — different sport root than team sports.
- Tennis scoreboard varies by tournament (slams vs. regular tour). ESPN groups by event.
- PGA Golf leaderboard uses `sports/golf/pga` — different parsing (cut line, round scores).
- Rugby scoreboard uses event-based format similar to UFC.
- WNBA uses same basketball parsing as NBA.
- The Odds API returns empty `[]` for off-season sports. Check `active` field in `/v4/sports/` before fetching odds. Don't treat empty results as an error — inform the user the sport is out of season.
- The Odds API key must be read from `~/.hermes/skills/tools/sports-scores/.env`. NEVER hardcode it in commands or URLs that might appear in logs or session transcripts.
- The Odds API free tier allows 500 requests/month. Don't re-fetch the full sport list every query — cache the active sports mentally per session if possible.
- Soccer odds use 3-way h2h (home/draw/away). US sports (NBA, NFL, MLB, NHL) use 2-way h2h (no draw). The parsing handles both — outcomes list length varies.
- When user asks "odds for Barcelona" and La Liga is off-season, check Copa Libertadores as a fallback — South American seasons run year-round and often feature Brazilian/Argentine clubs Barça fans follow.
- **The Odds API has zero motorsport coverage.** No F1, IndyCar, NASCAR, MotoGP, or any racing — not active, not inactive, simply absent from the 164-sport catalog. If a user asks for F1 odds, state this directly. Do not attempt an Odds API fetch for any motorsport.
- **Test before push.** When adding a new data source or feature to this skill, test all claimed capabilities against the live API before committing and pushing to GitHub. An untested push that advertises F1 odds support would be worse than no push — it creates a false promise in the repo. Verify each sport key returns live data; if a sport is off-season, confirm the empty-result behavior is clean, then test at least one active sport end-to-end.