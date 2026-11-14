# Data

Our project looks at whether NBA teams copy championship-winning teams. We want to study roster construction, player characteristics, salaries, and playing styles.

The `data/` folder currently contains **six CSV files**. Each one gives us different information for the project.

---

## 1. `nba_champions.csv`

**What it contains:** The NBA champion for each season.

- Rows: 30
- Columns: 4
- Seasons: 1996–97 to 2025–26
- Source: NBA historical championship records

Each row represents one season and its championship-winning team.

| Column | What it means |
|---|---|
| `SEASON` | NBA season (e.g., 2023-24). |
| `TEAM_ID` | Unique ID for the team. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation (e.g., BOS, LAL, GSW). |
| `TEAM_NAME` | Full team name. |

**How we use it:** Identifies the champions so we can compare them with other teams and see whether other franchises start adopting similar playing styles or roster strategies.

---

## 2. `nba_teams.csv`

**What it contains:** Basic information about all 30 current NBA teams.

- Rows: 30
- Columns: 3
- Source: NBA team information from `nba_api`

| Column | What it means |
|---|---|
| `TEAM_ID` | Unique ID for the team. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `TEAM_NAME` | Full team name. |

**How we use it:** Mainly used as a reference when connecting different datasets using team IDs.

**Important:** This only contains the 30 current NBA teams. It does not include the full history of old team names, locations, or franchise changes.

---

## 3. `team_season_stats_clean.csv`

**What it contains:** Team-wide regular-season statistics.

- Rows: 480
- Columns: 71
- Seasons: 2010–11 to 2025–26
- Coverage: 30 teams per season
- Source: NBA.com through `nba_api`

Each row represents one team's performance for one regular season. For example, Boston has one row for 2022–23 and another for 2023–24.

This dataset includes:
- Traditional team stats
- Advanced team stats
- Opponent stats

### Column descriptions

**Team information**

| Column | What it means |
|---|---|
| `SEASON` | NBA season. |
| `TEAM_ID` | Unique team ID. |
| `TEAM_ABBREVIATION` | Team abbreviation. |
| `TEAM_NAME` | Full team name. |

**Traditional statistics**

| Columns | What they mean |
|---|---|
| `GP`, `W`, `L` | Games played, wins, and losses. |
| `W_PCT` | Winning percentage. |
| `MIN` | Minutes played per game. |
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and percentage. |
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds. |
| `AST`, `TOV` | Assists and turnovers. |
| `STL`, `BLK` | Steals and blocks. |
| `BLKA` | Blocked field goal attempts. |
| `PF`, `PFD` | Fouls committed and fouls drawn. |
| `PTS` | Points scored per game. |
| `PLUS_MINUS` | Average point difference between the team and its opponents. |

**Advanced statistics**

| Columns | What they mean |
|---|---|
| `E_OFF_RATING`, `OFF_RATING` | Estimated and standard offensive rating. |
| `E_DEF_RATING`, `DEF_RATING` | Estimated and standard defensive rating. |
| `E_NET_RATING`, `NET_RATING` | Estimated and standard net rating. |
| `AST_PCT` | Percentage of made field goals assisted. |
| `AST_TO` | Assist-to-turnover ratio. |
| `AST_RATIO` | Assists per 100 possessions. |
| `OREB_PCT`, `DREB_PCT`, `REB_PCT` | Offensive, defensive, and total rebound percentages. |
| `TM_TOV_PCT` | Team turnover percentage. |
| `EFG_PCT` | Effective field goal percentage, which accounts for three-pointers. |
| `TS_PCT` | True shooting percentage, which accounts for field goals, three-pointers, and free throws. |
| `E_PACE`, `PACE` | Estimated and standard pace (possessions per 48 minutes). |
| `PACE_PER40` | Pace adjusted to a 40-minute game. |
| `POSS` | Estimated total possessions. |
| `PIE` | Player Impact Estimate at the team level. |

**Opponent statistics**

These show what opponents averaged against each team during the season.

| Columns | What they mean |
|---|---|
| `OPP_FGM`, `OPP_FGA`, `OPP_FG_PCT` | Opponent field goals made, attempted, and percentage. |
| `OPP_FG3M`, `OPP_FG3A`, `OPP_FG3_PCT` | Opponent three-pointers made, attempted, and percentage. |
| `OPP_FTM`, `OPP_FTA`, `OPP_FT_PCT` | Opponent free throws made, attempted, and percentage. |
| `OPP_OREB`, `OPP_DREB`, `OPP_REB` | Opponent offensive, defensive, and total rebounds. |
| `OPP_AST`, `OPP_TOV` | Opponent assists and turnovers. |
| `OPP_STL`, `OPP_BLK`, `OPP_BLKA` | Opponent steals, blocks, and blocked field goal attempts. |
| `OPP_PF`, `OPP_PFD` | Opponent fouls committed and drawn. |
| `OPP_PTS` | Opponent points per game. |
| `PLUS_MINUS_OPP` | Point differential measure returned with the opponent statistics. |

**How we use it:** This is one of our main datasets for comparing team playing styles. For example, we can compare three-point attempts, pace, offensive rating, defensive rating, and shooting efficiency between champions and other teams.

**Important notes:**
- These are team-wide statistics, not individual player stats.
- Most traditional stats are averages per game. Other columns are percentages, rates, or totals.
- Opponent stats are season averages, not individual game records.
- Some seasons had fewer games because of shortened seasons. Keep this in mind when comparing seasons.

---

## 4. `nba_rosters.csv`

**What it contains:** Player roster information for NBA teams.

- Rows: 7,747
- Columns: 17
- Seasons: 2010–11 to 2025–26
- Source: NBA.com through the `CommonTeamRoster` endpoint in `nba_api`

Each row represents a player associated with a team during a season.

### Column descriptions

| Column | What it means |
|---|---|
| `SEASON` | NBA season. |
| `TEAM_ID` | Unique team ID. |
| `TEAM_ABBREVIATION` | Team abbreviation. |
| `TEAM_NAME` | Full team name. |
| `PLAYER_ID` | Unique player ID. |
| `PLAYER` | Player's full name. |
| `NICKNAME` | Player's nickname. |
| `PLAYER_SLUG` | NBA player URL identifier. |
| `NUM` | Jersey number. |
| `POSITION` | Player's position (G, F, C, or combinations like G-F). |
| `HEIGHT` | Player's height. |
| `WEIGHT` | Player's weight. |
| `BIRTH_DATE` | Player's date of birth. |
| `AGE` | Player's age. |
| `EXP` | Years of NBA experience. `R` means rookie. |
| `SCHOOL` | College or school attended. |
| `HOW_ACQUIRED` | How the player joined the team, when available. |

**How we use it:** Helps us compare roster construction, such as player ages, experience, positions, and other player characteristics.

**Important notes:**
- This dataset gives us roster information, not player performance stats. Those are in `player_regular_season_stats.csv`.
- Some fields have missing values. `HOW_ACQUIRED` is missing for many players.
- `EXP` uses `R` for rookies. We can convert this to `0` for numerical analysis.
- **The roster endpoint does not consistently show every team a traded player played for during a season.** We tested this using Buddy Hield. He played for Indiana and Philadelphia in 2023–24, but the endpoint only returned Philadelphia, even after we checked all 30 teams.
- Because of this, we should not treat this file as a complete history of every player's team changes.

---

## 5. `player_regular_season_stats.csv`

**What it contains:** Individual player regular-season statistics.

- Rows: 8,341
- Columns: 36
- Seasons: 2010–11 to 2025–26
- Source: NBA.com through the `LeagueDashPlayerStats` endpoint in `nba_api`
- Type: Regular season
- Format: Per-game statistics for the selected PerGame measures.

Each row represents one player's statistics for a season.

### Column descriptions

**Player and team information**

| Column | What it means |
|---|---|
| `SEASON` | NBA season. |
| `PLAYER_ID` | Unique player ID. |
| `PLAYER_NAME` | Player's full name. |
| `NICKNAME` | Player's nickname. |
| `TEAM_ID` | Team ID returned by the stats endpoint. |
| `TEAM_ABBREVIATION` | Team abbreviation returned by the endpoint. |
| `AGE` | Player's age during the season. |

**Games and playing time**

| Columns | What they mean |
|---|---|
| `GP` | Games played. |
| `W`, `L` | Team wins and losses in games the player appeared in. |
| `W_PCT` | Winning percentage in games the player appeared in. |
| `MIN` | Average minutes played per game. |

**Scoring and shooting**

| Columns | What they mean |
|---|---|
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and percentage. |
| `PTS` | Points per game. |

**Rebounding and playmaking**

| Columns | What they mean |
|---|---|
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds per game. |
| `AST` | Assists per game. |
| `TOV` | Turnovers per game. |

**Defense and other stats**

| Columns | What they mean |
|---|---|
| `STL` | Steals per game. |
| `BLK` | Blocks per game. |
| `BLKA` | Blocked field goal attempts per game. |
| `PF` | Personal fouls per game. |
| `PFD` | Personal fouls drawn per game. |
| `PLUS_MINUS` | Average point differential while the player is on the court. |
| `DD2` | Number of double-doubles. |
| `TD3` | Number of triple-doubles. |

**Other information**

| Column | What it means |
|---|---|
| `TEAM_COUNT` | Number of teams associated with the player during that season, according to the NBA stats endpoint. |

**How we use it:** Helps us compare the types of players championship teams have. We can look at scoring, shooting, rebounding, assists, and defense to see whether other teams build similar player profiles.

**Important notes:**
- These are individual player stats, not team-wide averages.
- Most of the stats are per-game averages. `GP` tells us how many games the player appeared in.
- Each player has one season-level record, not a separate stats record for every team they played for.
- `TEAM_COUNT` tells us how many teams a player represented, but does not tell us which teams.
- Example: Buddy Hield's 2023–24 record shows Philadelphia, `TEAM_COUNT = 2`, and 84 games played, even though he also played for Indiana.
- Do not assume that all of a player's season stats belong to the team listed in `TEAM_ABBREVIATION`.

---

## 6. `nba_team_game_stats.csv`

**What it contains:** Game-by-game regular-season statistics for every NBA team.

- Rows: 38,238
- Columns: 31
- Unique games: 19,119
- Seasons: 2010–11 to 2025–26
- Coverage: All 30 NBA teams
- Source: NBA.com through the `LeagueGameLog` endpoint in `nba_api`
- Type: Regular season

**Each row represents one team's performance in one game.**

There are two rows for every game: one for each team. For example, if Boston plays Los Angeles, one row shows Boston's stats and the other shows Los Angeles's stats.

### Column descriptions

**Game and team information**

| Column | What it means |
|---|---|
| `SEASON` | NBA season. |
| `SEASON_ID` | NBA season identifier returned by the API. |
| `GAME_ID` | Unique ID for the game. Both teams share the same game ID. |
| `GAME_DATE` | Date of the game. |
| `TEAM_ID` | Unique ID for the team in that row. |
| `TEAM_ABBREVIATION` | Team abbreviation. |
| `TEAM_NAME` | Full team name. |
| `OPPONENT` | Opposing team's abbreviation. |
| `MATCHUP` | Shows the matchup and whether the team played at home or away. |
| `WL` | Whether the team won (`W`) or lost (`L`). |

**Game statistics**

| Columns | What they mean |
|---|---|
| `MIN` | Minutes played. |
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and percentage. |
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds. |
| `AST` | Assists. |
| `STL` | Steals. |
| `BLK` | Blocks. |
| `TOV` | Turnovers. |
| `PF` | Personal fouls. |
| `PTS` | Points scored. |
| `PLUS_MINUS` | Point difference for that team in the game. |
| `VIDEO_AVAILABLE` | Indicates whether a video is available through the NBA stats endpoint. |

**How we use it:** Lets us look at individual game results instead of only season averages. We can check head-to-head records, see how teams performed against champions, calculate win streaks, and track team performance over time.

**Important notes:**
- This is regular-season data only. Playoff games are not included.
- Each game has two rows, one for each team. Both rows share the same `GAME_ID`.
- There are 38,238 rows representing 19,119 games.
- Some seasons have fewer games because of shortened NBA seasons.
- A few shooting percentage or win/loss fields have missing values. We should inspect those before using them, but we do not need to delete entire rows automatically.

---

## General notes

A few things to remember when using the datasets:

- `team_season_stats_clean.csv` shows team-wide season performance.
- `player_regular_season_stats.csv` shows individual player performance.
- `nba_rosters.csv` shows roster information.
- `nba_team_game_stats.csv` shows what happened in each individual regular-season game.
- `nba_champions.csv` tells us who won each championship.
- `nba_teams.csv` helps us connect team IDs, abbreviations, and names.

**Roster and player stats differences:**

The roster dataset has 7,747 rows, while the player stats dataset has 8,341 rows. We compared them and found 725 unique player-season combinations in the player stats dataset that did not match a player-season combination in the roster dataset.

We also checked 1,093 player-season records where `TEAM_COUNT` was greater than 1:
- 984 had only one team association in the roster dataset.
- 109 had no matching roster record.
- None had multiple team associations recorded.

We tested the NBA roster endpoint again using Buddy Hield and found that it only returned Philadelphia for 2023–24, even though he also played for Indiana.

For now, we are keeping both datasets. We just need to be careful when connecting player stats to teams, especially for players who were traded during a season.

**Time period:** The championship dataset covers 1996–97 through 2025–26. The other five datasets cover 2010–11 through 2025–26. Any analysis combining them will use the overlapping seasons unless we collect more historical data.