## Data

This project uses NBA data to investigate whether teams imitate championship-winning franchises in their roster construction, player characteristics, salary allocation, and playing styles.

The `data/` folder currently contains four CSV files. Each dataset serves a different purpose, and together they provide information about championship history, team performance, and player roster composition.

### 1. `nba_champions.csv`

**Purpose:** Records the NBA champion for each season.

- **Rows:** 30
- **Columns:** 4
- **Time period:** 1996–97 through 2025–26
- **Source:** NBA historical championship records

Each row represents one NBA championship season and identifies the team that won the title.

| Column | Description |
|---|---|
| `SEASON` | NBA season, formatted as YYYY-YY (e.g., 2023-24). |
| `TEAM_ID` | NBA's unique numerical identifier for the champion. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation (e.g., BOS, LAL, GSW). |
| `TEAM_NAME` | Full name of the championship-winning team. |

**How we will use it:** This file identifies championship teams so we can compare their statistics and characteristics with other teams in the same season and examine whether other franchises adopt similar approaches.

### 2. `nba_teams.csv`

**Purpose:** Provides a reference table connecting NBA team IDs, abbreviations, and team names.

- **Rows:** 30
- **Columns:** 3
- **Coverage:** The 30 current NBA teams
- **Source:** `nba_api` static NBA team information

Each row represents one current NBA franchise.

| Column | Description |
|---|---|
| `TEAM_ID` | NBA's unique numerical identifier for the team. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation (e.g., NYK, DEN, MIL). |
| `TEAM_NAME` | Full team name (e.g., New York Knicks, Denver Nuggets, Milwaukee Bucks). |

**How we will use it:** This file acts as a lookup table. NBA statistical endpoints often provide team IDs and names, so this reference allows us to connect team IDs to abbreviations and consistently merge datasets.

**Important:** This table represents current NBA teams, not a complete history of every franchise name or location. Historical team identities and relocations may require additional handling when working with older seasons.

### 3. `team_season_stats_clean.csv`

**Purpose:** Contains team-level regular-season statistics for every NBA team across multiple seasons.

- **Rows:** 480
- **Columns:** 71
- **Time period:** 2010–11 through 2025–26
- **Coverage:** 30 teams per season across 16 seasons
- **Source:** NBA.com statistics, collected using the `nba_api` Python package

Each row represents **one team's performance during one regular season**. For example, the Boston Celtics in 2022–23 have one row, while the Celtics in 2023–24 have a separate row.

The dataset combines three statistical categories from the NBA team statistics endpoint:

- **Base statistics:** Traditional team statistics, including wins, losses, shooting, scoring, rebounding, assists, turnovers, and other box-score measures.
- **Advanced statistics:** More detailed measures of team performance and playing style, including offensive rating, defensive rating, net rating, pace, true shooting percentage, assist percentage, and other efficiency metrics.
- **Opponent statistics:** Season-level averages of what opposing teams produced against each team. These include opponent points, field goals, three-pointers, rebounds, assists, turnovers, and other measures. These are aggregated across the season, not individual game records.

#### Column descriptions

**Team identification**

| Column | Description |
|---|---|
| `SEASON` | NBA season. |
| `TEAM_ID` | Unique NBA team identifier. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `TEAM_NAME` | Full team name. |

**Traditional team performance**

| Columns | Description |
|---|---|
| `GP`, `W`, `L` | Games played, wins, and losses. |
| `W_PCT` | Winning percentage. |
| `MIN` | Average minutes played per game. |
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and field goal percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and three-point percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and free throw percentage. |
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds. |
| `AST`, `TOV` | Assists and turnovers. |
| `STL`, `BLK` | Steals and blocks. |
| `BLKA` | Blocked field goal attempts. |
| `PF`, `PFD` | Personal fouls committed and personal fouls drawn. |
| `PTS` | Points scored per game. |
| `PLUS_MINUS` | Average point differential per game. |

**Advanced team performance and playing style**

| Columns | Description |
|---|---|
| `E_OFF_RATING`, `OFF_RATING` | Estimated and standard offensive rating. |
| `E_DEF_RATING`, `DEF_RATING` | Estimated and standard defensive rating. |
| `E_NET_RATING`, `NET_RATING` | Estimated and standard net rating. |
| `AST_PCT` | Percentage of made field goals assisted. |
| `AST_TO` | Assist-to-turnover ratio. |
| `AST_RATIO` | Assists per 100 possessions. |
| `OREB_PCT`, `DREB_PCT`, `REB_PCT` | Offensive, defensive, and total rebound percentages. |
| `TM_TOV_PCT` | Team turnover percentage. |
| `EFG_PCT` | Effective field goal percentage, accounting for the added value of three-pointers. |
| `TS_PCT` | True shooting percentage, accounting for field goals, three-pointers, and free throws. |
| `E_PACE`, `PACE` | Estimated and standard pace, measuring possessions per 48 minutes. |
| `PACE_PER40` | Pace adjusted to a 40-minute game. |
| `POSS` | Total estimated possessions. |
| `PIE` | Player Impact Estimate at the team level, measuring a team's share of game statistical production. |

**Opponent statistics**

These columns represent what opponents averaged against the team during that season.

| Columns | Description |
|---|---|
| `OPP_FGM`, `OPP_FGA`, `OPP_FG_PCT` | Opponent field goals made, attempted, and field goal percentage. |
| `OPP_FG3M`, `OPP_FG3A`, `OPP_FG3_PCT` | Opponent three-pointers made, attempted, and three-point percentage. |
| `OPP_FTM`, `OPP_FTA`, `OPP_FT_PCT` | Opponent free throws made, attempted, and free throw percentage. |
| `OPP_OREB`, `OPP_DREB`, `OPP_REB` | Opponent offensive, defensive, and total rebounds. |
| `OPP_AST`, `OPP_TOV` | Opponent assists and turnovers. |
| `OPP_STL`, `OPP_BLK`, `OPP_BLKA` | Opponent steals, blocks, and blocked field goal attempts. |
| `OPP_PF`, `OPP_PFD` | Opponent personal fouls committed and drawn. |
| `OPP_PTS` | Points scored per game by opponents. |
| `PLUS_MINUS_OPP` | Point differential measure returned with the opponent statistics. |

**How we will use it:** This is the main dataset for comparing team performance and playing styles across seasons. We can use it to identify statistical patterns among championship teams, compare those patterns with other franchises, and investigate whether teams change their playing styles after a championship team succeeds.

### 4. `nba_rosters.csv`

**Purpose:** Contains player roster information for every NBA team across multiple seasons.

- **Rows:** 7,747
- **Columns:** 17
- **Time period:** 2010–11 through 2025–26
- **Coverage:** All 30 NBA teams across 16 seasons
- **Source:** NBA.com statistics, collected using the `nba_api` Python package and the `CommonTeamRoster` endpoint.

Each row represents **one player associated with one team during one season**. Players who played for multiple teams during a season can appear more than once, once for each team.

#### Column descriptions

| Column | Description |
|---|---|
| `SEASON` | NBA season, formatted as YYYY-YY. |
| `TEAM_ID` | Unique NBA team identifier. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `TEAM_NAME` | Full name of the team. |
| `PLAYER_ID` | Unique NBA player identifier. |
| `PLAYER` | Player's full name. |
| `NICKNAME` | Player's nickname. |
| `PLAYER_SLUG` | NBA player URL identifier. |
| `NUM` | Player's jersey number. |
| `POSITION` | Player's listed position (G, F, C, or combinations such as G-F and F-C). |
| `HEIGHT` | Player's listed height. |
| `WEIGHT` | Player's listed weight. |
| `BIRTH_DATE` | Player's date of birth. |
| `AGE` | Player's age. |
| `EXP` | Years of NBA experience. The value `R` indicates a rookie. |
| `SCHOOL` | College or school attended. |
| `HOW_ACQUIRED` | How the player joined the team, when information is available. |

**How we will use it:** This dataset will help us examine roster construction and player characteristics across teams and seasons. We can compare championship teams with other franchises based on average player age, experience, positional distribution, and roster composition. It can also help us investigate whether teams retain similar groups of players or acquire players with characteristics resembling those of successful championship teams.

### Important notes about the current data

- `team_season_stats_clean.csv` contains **regular-season team averages and season-level measures**, not individual game records.
- `nba_rosters.csv` contains roster information, not individual player performance statistics. Player statistics will be collected separately.
- Many traditional team box-score statistics are reported on a per-game basis. Other measures, such as total possessions, are season-level totals or percentages/rates.
- The opponent statistics in the team dataset are season aggregates, not separate rows for each opponent or game.
- In the roster dataset, `EXP` uses `R` to indicate a rookie (zero years of prior NBA experience). For numerical analysis, this value can be converted to `0` while preserving the original column.
- Some roster fields contain missing values. In particular, `HOW_ACQUIRED` is unavailable for many players, so it should be used cautiously in analysis.
- Players who appeared for multiple teams in the same season may have multiple records in `nba_rosters.csv`. This is intentional because each record represents a player-team-season combination.
- The championship history covers 1996–97 through 2025–26, while the team statistics and roster datasets currently cover 2010–11 through 2025–26. Analyses combining these datasets will therefore be limited to the overlapping seasons unless additional historical data is collected.

### Planned additional datasets

| Dataset | What it will contain | Why it matters |
|---|---|---|
| `player_season_stats.csv` | Individual player statistics for each season and team, including scoring, rebounding, assists, shooting efficiency, minutes, and advanced metrics. | Helps compare player production, roles, and contributions to team success. |
| `game_stats.csv` | Team performance in individual games. | Allows us to study changes in performance over time and before or after championship seasons. |
| Salary data | Player salaries and team payroll information. | Helps compare how championship teams allocate salary across their rosters. |

Together, these datasets will allow us to investigate whether NBA franchises copy successful championship teams in terms of playing style, player composition, player performance, and salary allocation.