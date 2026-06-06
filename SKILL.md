---
name: sports-scores
description: Live scores, standings, and F1 data from ESPN and Ergast APIs. No API keys required.
version: 1.0.0
author: Cipher
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [sports, scores, nba, nfl, mlb, nhl, soccer, f1, espn, live, standings]
    category: tools
    requires_toolsets: [terminal]
---

# Sports Scores

Live scores, standings, and F1 data from free public APIs. No API keys required.

## When to Use

- User asks about any sports score, game result, or standings
- User asks "how did [team] do" or "what's the score"
- User asks about F1 race results, driver standings, or next race
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
| Live timing | `https://api.openf1.org/v1/position?session_key=latest` |

## Sport Detection

Map the user's question to the right endpoint:

| Keywords | Sport | League Code |
|----------|-------|-------------|
| nba, basketball, knicks, lakers, celtics, warriors, bucks, etc. | Basketball | nba |
| nfl, football, superbowl, chiefs, 49ers, cowboys, patriots, etc. | Football | nfl |
| mlb, baseball, yankees, dodgers, mets, red sox, etc. | Baseball | mlb |
| nhl, hockey, rangers, avalanche, panthers, oilers, etc. | Hockey | nhl |
| la liga, barcelona, barca, real madrid, atletico, spanish league | Soccer | esp.1 |
| premier league, epl, manchester, liverpool, arsenal, chelsea, english league | Soccer | eng.1 |
| champions league, ucl, champions | Soccer | UEFA.CHAMPIONS |
| mls, inter miami, lafc, american soccer | Soccer | usa.1 |
| world cup, fifa, fifa world cup, mundial | Soccer | fifa.world |
| bundesliga, bayern, dortmund, german league | Soccer | ger.1 |
| serie a, ac milan, inter, juve, juventus, italian league | Soccer | ita.1 |
| ligue 1, psg, paris saint-germain, french league | Soccer | fra.1 |
| liga mx, mexican league, club america, chivas | Soccer | mex.1 |
| copa libertadores, libertadores | Soccer | CONMEBOL.LIBERTADORES |
| ufc, mma, ufc fight night, octagon | MMA | ufc |
| tennis, atp, wta, wimbledon, roland garros, us open tennis, australian open | Tennis | tennis |
| golf, pga, masters, pga tour | Golf | pga |
| rugby, rugby world cup, six nations | Rugby | rugby |
| wnba, women's basketball | Basketball | wnba |
| f1, formula 1, formula one, grand prix, gp, race, verstappen, hamilton, leclerc, etc. | F1 | f1 |

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

For Premier League, replace `esp.1` with `eng.1` in the URL. For Champions League, replace `esp.1` with `UEFA.CHAMPIONS`. For Bundesliga, use `ger.1`. For Serie A, use `ita.1`. For Ligue 1, use `fra.1`.

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

## Output Rules

1. **Clean format.** Never dump raw JSON. Parse and present human-readable summaries.
2. **Live games.** If a game status is "In Progress" or similar, clearly note it: **LIVE**.
3. **Scheduled games.** Show date, time, and broadcast info.
4. **Completed games.** Show final score with winner bold or marked.
5. **Standings.** Top 10 only unless user asks for full table.
6. **F1.** Show driver name, constructor, position, and points/gap.
7. **Time zones.** Always show times in the user's local timezone. Convert from UTC when needed.
8. **Multiple games.** If asking about a league, show all games for today. If asking about a team, show just that team's game.
9. **No API keys.** All endpoints are free and keyless. If one fails, report the error — don't substitute a paid API.

## Sport-Specific Notes

### NBA
- Playoff brackets: ESPN doesn't have a clean bracket endpoint. For playoff series, use the scoreboard and look for series summaries.
- Standings use Eastern/Western conference split.

### NFL
- NFL season is Sept–Feb. Off-season queries will return empty scoreboards.
- Standings use AFC/NFC conference split.

### Soccer
- La Liga, Premier League, Champions League, Bundesliga, Serie A, Ligue 1, Liga MX, Copa Libertadores, MLS, and FIFA World Cup are supported.
- Soccer scoreboards show matchday groupings. Parse `competitions[0].competitors` for scores.

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
| "Is there a hockey game on" | Fetch NHL scoreboard, show schedule |

## Pitfalls

- ESPN API responses are large. Use `python3 -c` to parse inline — don't dump full JSON.
- Soccer league codes are not intuitive: `esp.1` (La Liga), `eng.1` (Premier League), `UEFA.CHAMPIONS` (Champions League), `usa.1` (MLS), `ger.1` (Bundesliga), `ita.1` (Serie A), `fra.1` (Ligue 1). Always use the exact codes.
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