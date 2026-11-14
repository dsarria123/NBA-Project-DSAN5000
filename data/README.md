# Data

Our project uses NBA data to investigate whether teams copy championship-winning teams. We want to look at roster construction, player characteristics, salary allocation, and playing styles.

The `data/` folder currently contains five CSV files. Each dataset gives us a different piece of information that we can use for our analysis.

---

## 1. `nba_champions.csv`

**Purpose:** Keeps track of which team won the NBA championship each season.

- **Rows:** 30
- **Columns:** 4
- **Seasons:** 1996–97 through 2025–26
- **Source:** NBA historical championship records

Each row represents one NBA season and its championship-winning team.

| Column | Description |
|---|---|
| `SEASON` | NBA season (e.g., 2023-24). |
| `TEAM_ID` | Unique NBA ID for the team. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation (e.g., BOS, LAL, GSW). |
| `TEAM_NAME` | Full name of the championship-winning team. |

**How we will use it:**

This is our reference for identifying championship teams. We can compare champions with other teams during the same season and look at whether other franchises start adopting similar strategies or characteristics.

---

## 2. `nba_teams.csv`

**Purpose:** Contains basic information about NBA teams, including their IDs, abbreviations, and names.

- **Rows:** 30
- **Columns:** 3
- **Coverage:** All 30 current NBA teams
- **Source:** NBA team information from the `nba_api` Python package.

Each row represents one current NBA team.

| Column | Description |
|---|---|
| `TEAM_ID` | Unique NBA ID for the team. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation (e.g., NYK, DEN, MIL). |
| `TEAM_NAME` | Full team name (e.g., New York Knicks). |

**How we will use it:**

This dataset is mainly a reference table. It helps us connect team IDs to team names and abbreviations when combining different datasets.

**Important note:**

This file only contains the 30 current NBA teams. It does not include a complete history of old team names, locations, or franchise changes. We may need to account for historical changes when working with older seasons.

---

## 3. `team_season_stats_clean.csv`

**Purpose:** Contains team-level regular-season statistics for all 30 NBA teams across multiple seasons.

- **Rows:** 480
- **Columns:** 71
- **Seasons:** 2010–11 through 2025–26
- **Coverage:** 30 teams per season across 16 seasons
- **Source:** NBA.com statistics, collected using the `nba_api` Python package.

Each row represents one team's performance during one regular season. For example, Boston in 2022–23 has one row, and Boston in 2023–24 has another.

This dataset combines three types of statistics:

1. **Base statistics:** Traditional team stats such as wins, losses, shooting, scoring, rebounds, assists, and turnovers.
2. **Advanced statistics:** More detailed measures of team performance and playing style, such as offensive rating, defensive rating, net rating, pace, and shooting efficiency.
3. **Opponent statistics:** Statistics showing what opposing teams averaged against each team during the season.

### Column descriptions

**Team identification**

| Column | Description |
|---|---|
| `SEASON` | NBA season. |
| `TEAM_ID` | Unique NBA team ID. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `TEAM_NAME` | Full team name. |

**Traditional team statistics**

| Columns | Description |
|---|---|
| `GP`, `W`, `L` | Games played, wins, and losses. |
| `W_PCT` | Team winning percentage. |
| `MIN` | Average minutes played per game. |
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and shooting percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and three-point percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and free throw percentage. |
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds. |
| `AST`, `TOV` | Assists and turnovers. |
| `STL`, `BLK` | Steals and blocks. |
| `BLKA` | Blocked field goal attempts. |
| `PF`, `PFD` | Personal fouls committed and drawn. |
| `PTS` | Points scored per game. |
| `PLUS_MINUS` | Average point differential per game. |

**Advanced statistics**

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
| `POSS` | Estimated total possessions. |
| `PIE` | Player Impact Estimate at the team level, measuring the team's share of game statistical production. |

**Opponent statistics**

These columns show what opposing teams averaged against each team during the season.

| Columns | Description |
|---|---|
| `OPP_FGM`, `OPP_FGA`, `OPP_FG_PCT` | Opponent field goals made, attempted, and shooting percentage. |
| `OPP_FG3M`, `OPP_FG3A`, `OPP_FG3_PCT` | Opponent three-pointers made, attempted, and percentage. |
| `OPP_FTM`, `OPP_FTA`, `OPP_FT_PCT` | Opponent free throws made, attempted, and percentage. |
| `OPP_OREB`, `OPP_DREB`, `OPP_REB` | Opponent offensive, defensive, and total rebounds. |
| `OPP_AST`, `OPP_TOV` | Opponent assists and turnovers. |
| `OPP_STL`, `OPP_BLK`, `OPP_BLKA` | Opponent steals, blocks, and blocked field goal attempts. |
| `OPP_PF`, `OPP_PFD` | Opponent personal fouls committed and drawn. |
| `OPP_PTS` | Opponent points scored per game. |
| `PLUS_MINUS_OPP` | Point differential measure returned with the opponent statistics. |

**How we will use it:**

This is one of our main datasets for studying whether teams copy the playing styles of championship teams. We can compare things like three-point attempts, pace, offensive rating, defensive rating, and shooting efficiency across teams and seasons.

**Important notes:**

- These are team-level statistics, not individual player statistics.
- Most traditional box-score statistics are reported per game. Other measures are percentages, rates, or season totals.
- Opponent statistics are season averages, not separate records for each game or opponent.
- Some seasons have fewer games than others because of shortened seasons and other scheduling differences. We should keep this in mind when comparing statistics across years.

---

## 4. `nba_rosters.csv`

**Purpose:** Contains player roster information for NBA teams across multiple seasons.

- **Rows:** 7,747
- **Columns:** 17
- **Seasons:** 2010–11 through 2025–26
- **Coverage:** All 30 NBA teams across 16 seasons
- **Source:** NBA.com statistics, collected using the `nba_api` Python package and the `CommonTeamRoster` endpoint.

Each row represents a player associated with a team during a particular season.

### Column descriptions

| Column | Description |
|---|---|
| `SEASON` | NBA season (e.g., 2023-24). |
| `TEAM_ID` | Unique NBA team ID. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `TEAM_NAME` | Full team name. |
| `PLAYER_ID` | Unique NBA player ID. |
| `PLAYER` | Player's full name. |
| `NICKNAME` | Player's nickname. |
| `PLAYER_SLUG` | NBA player URL identifier. |
| `NUM` | Player's jersey number. |
| `POSITION` | Listed position (G, F, C, or combinations like G-F and F-C). |
| `HEIGHT` | Player's listed height. |
| `WEIGHT` | Player's listed weight. |
| `BIRTH_DATE` | Player's date of birth. |
| `AGE` | Player's age. |
| `EXP` | Years of NBA experience. `R` means rookie. |
| `SCHOOL` | College or school attended. |
| `HOW_ACQUIRED` | How the player joined the team, when available. |

**How we will use it:**

This dataset helps us study how teams build their rosters. We can compare championship teams with other teams based on player age, experience, positions, and roster composition.

**Important notes and limitations:**

- This dataset contains roster information, not individual player performance statistics. Those are in `player_regular_season_stats.csv`.
- Some columns have missing values. In particular, `HOW_ACQUIRED` is missing for many players, so we should be careful when using it.
- `EXP` uses `R` to identify rookies. For numerical analysis, we can convert `R` to `0` while keeping the original column.
- **The roster data does not consistently capture every team a traded player played for during a season.** We originally collected rosters by querying all 30 teams, but testing the `CommonTeamRoster` endpoint showed that it may only return one team association for a traded player.
- For example, Buddy Hield played for Indiana and Philadelphia in 2023–24, but our roster dataset only returned Philadelphia. We tested the endpoint again for all 30 teams and got the same result.
- Because of this, we should not assume that this file contains a complete history of every player's team associations during a season.

---

## 5. `player_regular_season_stats.csv`

**Purpose:** Contains individual player statistics for each NBA regular season.

- **Rows:** 8,341
- **Columns:** 36
- **Seasons:** 2010–11 through 2025–26
- **Coverage:** Players from all 30 NBA teams across 16 seasons
- **Source:** NBA.com statistics, collected using the `nba_api` Python package and the `LeagueDashPlayerStats` endpoint.
- **Season type:** Regular Season
- **Format:** Per-game statistics for the selected PerGame measures.

Each row represents one player's statistics for one season. This dataset gives us information about what individual players actually contributed on the court.

### Column descriptions

**Player and team identification**

| Column | Description |
|---|---|
| `SEASON` | NBA season. |
| `PLAYER_ID` | Unique NBA player ID. |
| `PLAYER_NAME` | Player's full name. |
| `NICKNAME` | Player's nickname. |
| `TEAM_ID` | NBA team ID returned by the statistics endpoint. |
| `TEAM_ABBREVIATION` | Three-letter team abbreviation. |
| `AGE` | Player's age during the season. |

**Games and playing time**

| Columns | Description |
|---|---|
| `GP` | Games played. |
| `W`, `L` | Team wins and losses in games the player appeared in. |
| `W_PCT` | Winning percentage in games the player appeared in. |
| `MIN` | Average minutes played per game. |

**Scoring and shooting**

| Columns | Description |
|---|---|
| `FGM`, `FGA`, `FG_PCT` | Field goals made, attempted, and shooting percentage. |
| `FG3M`, `FG3A`, `FG3_PCT` | Three-pointers made, attempted, and percentage. |
| `FTM`, `FTA`, `FT_PCT` | Free throws made, attempted, and percentage. |
| `PTS` | Points scored per game. |

**Rebounding and playmaking**

| Columns | Description |
|---|---|
| `OREB`, `DREB`, `REB` | Offensive, defensive, and total rebounds per game. |
| `AST` | Assists per game. |
| `TOV` | Turnovers per game. |

**Defense and other contributions**

| Columns | Description |
|---|---|
| `STL` | Steals per game. |
| `BLK` | Blocks per game. |
| `BLKA` | Blocked field goal attempts per game. |
| `PF` | Personal fouls per game. |
| `PFD` | Personal fouls drawn per game. |
| `PLUS_MINUS` | Average point differential while the player is on the court. |
| `DD2` | Double-doubles recorded. |
| `TD3` | Triple-doubles recorded. |

**Additional information**

| Column | Description |
|---|---|
| `TEAM_COUNT` | Number of teams associated with the player during that season, according to the NBA statistics endpoint. |

**How we will use it:**

This dataset helps us study the types of players championship teams have. We can compare scoring, shooting, rebounding, playmaking, and defensive contributions to see whether other teams build rosters with similar player profiles.

**Important notes and limitations:**

- These are individual player statistics, not team-wide averages.
- The statistics are per-game averages, while `GP` tells us how many games the player appeared in.
- Each player has one season-level record in this dataset, rather than separate statistical records for every team they played for.
- `TEAM_COUNT` helps identify players who represented multiple teams during a season, but it does not tell us which teams they played for.
- For example, Buddy Hield's 2023–24 record shows Philadelphia, `TEAM_COUNT = 2`, and 84 games played. He also played for Indiana that season.
- Because the statistics are season-level, we should not assume that all of a player's statistics belong to the team listed in `TEAM_ABBREVIATION`.

---

## Overall notes about the datasets

A few things to remember when working with these files:

- `team_season_stats_clean.csv` shows what teams did overall, while `player_regular_season_stats.csv` shows what individual players contributed.
- `nba_rosters.csv` gives us player information such as age, height, weight, experience, and position.
- The roster and player statistics datasets have different record counts: 7,747 rows in the roster dataset and 8,341 rows in the player statistics dataset.
- We compared the two datasets and found 725 unique player-season combinations in the player statistics dataset that did not match a player-season combination in the roster dataset.
- We also checked 1,093 player-season records where `TEAM_COUNT` was greater than 1. Of these, 984 had only one team association in the roster dataset, while 109 had no matching roster record. None had multiple team associations recorded.
- We tested the NBA roster endpoint again using Buddy Hield as an example. Even after checking all 30 teams, the endpoint only returned Philadelphia for his 2023–24 roster record, despite his having played for Indiana too.
- We are keeping both datasets as they are for now. The differences appear to come from how the NBA API endpoints return their data, not from intentionally removing players.
- We should be careful when merging the roster and player statistics datasets, especially for players who changed teams during a season.

**Time period note:** The championship dataset covers 1996–97 through 2025–26. The team statistics, roster, and player statistics datasets currently cover 2010–11 through 2025–26. Analyses that combine these datasets will therefore use the overlapping seasons unless we collect more historical data.