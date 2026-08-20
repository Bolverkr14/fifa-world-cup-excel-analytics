# Data Dictionary

## FIFA World Cup Analytics

## Purpose

This document describes the source datasets and the main fields used in the FIFA World Cup Analytics project.

The workbook contains four source datasets:

1. 2026 Team Summaries
2. Penalty Shootouts
3. 2026 Squads
4. FIFA World Cup Matches

The original data is stored in the `DATA_BRUT` worksheet. Cleaned and standardized data is stored in the `DATA_CLEANED` worksheet.

---

## 1. 2026 Team Summaries

This dataset contains summary information about the national teams included in the 2026 dataset.

### Country

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the national team.
- **Example:** `France`
- **Cleaning rules:** Country names are standardized using the project mapping table.

### 2026_Average_Age

- **Data type:** Decimal
- **Nullable:** No
- **Description:** Average age of the national team's 2026 squad.
- **Example:** `27.4`
- **Unit:** Years

### 2026_Unique_Clubs_Represented

- **Data type:** Integer
- **Nullable:** No
- **Description:** Number of different football clubs represented in the national squad.
- **Example:** `18`

### Historical_Matches_Played

- **Data type:** Integer
- **Nullable:** No
- **Description:** Total number of FIFA World Cup matches played by the national team before or within the source reference period.
- **Example:** `122`

### Historical_Goals_Scored

- **Data type:** Integer
- **Nullable:** No
- **Description:** Total number of FIFA World Cup goals scored by the national team.
- **Example:** `245`

---

## 2. Penalty Shootouts

This dataset contains individual penalty-kick records from FIFA World Cup penalty shootouts.

### Tournament_Year

- **Data type:** Integer
- **Nullable:** No
- **Description:** FIFA World Cup edition in which the penalty shootout took place.
- **Example:** `2022`

### Match_Stage

- **Data type:** Text
- **Nullable:** No
- **Description:** Tournament stage at which the penalty shootout occurred.
- **Example:** `Quarter-finals`
- **Standardized example:** `QUARTER_FINALS`

### Team_A

- **Data type:** Text
- **Nullable:** No
- **Description:** First national team involved in the penalty shootout.
- **Example:** `Argentina`

### Team_B

- **Data type:** Text
- **Nullable:** No
- **Description:** Second national team involved in the penalty shootout.
- **Example:** `Netherlands`

### Shooter_Team

- **Data type:** Text
- **Nullable:** No
- **Description:** National team of the player taking the penalty.
- **Example:** `Argentina`

### Shooter_Name

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the penalty taker.
- **Example:** `Lionel Messi`

### Goalkeeper_Name

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the goalkeeper facing the penalty kick.
- **Example:** `Andries Noppert`

### Kick_Number

- **Data type:** Integer
- **Nullable:** No
- **Description:** Overall chronological position of the kick within the penalty shootout.
- **Example:** `5`

### Team_Kick_Number

- **Data type:** Integer
- **Nullable:** No
- **Description:** Position of the kick within the shooter's own team sequence.
- **Example:** `3`

### Score_Before_Kick

- **Data type:** Text
- **Nullable:** No
- **Description:** Penalty shootout score before the kick was taken.
- **Example:** `3-2`

### Is_Must_Score

- **Data type:** Boolean
- **Nullable:** No
- **Description:** Indicates whether the player had to score to prevent immediate elimination.
- **Possible values:** `Yes`, `No`

### Is_Winning_Kick

- **Data type:** Boolean
- **Nullable:** No
- **Description:** Indicates whether the kick secured the team's victory.
- **Possible values:** `Yes`, `No`

### Shoot_Outcome

- **Data type:** Text
- **Nullable:** No
- **Description:** Outcome of the penalty kick.
- **Possible values:** `Goal`, `Miss`, `Missed`, `Saved`

---

## 3. 2026 Squads

This dataset contains player-level information for the national squads included in the 2026 source data.

### index

- **Data type:** Integer
- **Nullable:** No
- **Description:** Source row identifier.
- **Example:** `145`

### name

- **Data type:** Text
- **Nullable:** No
- **Description:** Player's full name.
- **Example:** `Kylian Mbappé`

### age

- **Data type:** Integer
- **Nullable:** No
- **Description:** Player's age in the 2026 squad data.
- **Example:** `27`
- **Unit:** Years

### country

- **Data type:** Text
- **Nullable:** No
- **Description:** National team represented by the player.
- **Example:** `France`

### position

- **Data type:** Text
- **Nullable:** No
- **Description:** Player's primary playing position.
- **Example:** `Forward`

### club

- **Data type:** Text
- **Nullable:** No
- **Description:** Player's professional club in the source dataset.
- **Example:** `Real Madrid`

### jersey_number

- **Data type:** Integer
- **Nullable:** No
- **Description:** Shirt number assigned to the player.
- **Example:** `10`

---

## 4. FIFA World Cup Matches

This dataset contains FIFA World Cup match results from 1930 to 2026.

### Year

- **Data type:** Integer
- **Nullable:** No
- **Description:** FIFA World Cup edition year.
- **Example:** `1998`

### Datetime

- **Data type:** Date and time
- **Nullable:** No
- **Description:** Date and scheduled time of the match.
- **Example:** `12 Jul 1998 - 21:00`

### Stage

- **Data type:** Text
- **Nullable:** No
- **Description:** Tournament stage at which the match was played.
- **Source example:** `Quarter-finals`
- **Standardized example:** `QUARTER_FINALS`

### Stadium

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the stadium where the match was played.
- **Example:** `Stade de France`

### City

- **Data type:** Text
- **Nullable:** No
- **Description:** Host city in which the match was played.
- **Example:** `Saint-Denis`

### Home Team Name

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the team listed as the home team.
- **Example:** `France`

### Home Team Goals

- **Data type:** Integer
- **Nullable:** No
- **Description:** Number of goals scored by the home team before the penalty shootout.
- **Example:** `3`

### Away Team Goals

- **Data type:** Integer
- **Nullable:** No
- **Description:** Number of goals scored by the away team before the penalty shootout.
- **Example:** `0`

### Away Team Name

- **Data type:** Text
- **Nullable:** No
- **Description:** Name of the team listed as the away team.
- **Example:** `Brazil`

### Win conditions

- **Data type:** Text
- **Nullable:** Yes
- **Description:** Additional information explaining how the match was decided.
- **Example:** `France won after extra time`
- **Possible information:** Extra time, penalty shootout, golden goal or no additional condition.

---

## Standardized Tournament Stages

The source data contains multiple names and formats for the same tournament stages. These values are standardized as follows:

- `Group 1`, `Group A`, `group stage` → `GROUP_STAGE`
- `Preliminary round`, `First round` → `GROUP_STAGE`
- `Round of 32` → `ROUND_OF_32`
- `Round of 16` → `ROUND_OF_16`
- `Quarter-finals` → `QUARTER_FINALS`
- `Semi-finals` → `SEMI_FINALS`
- `Third place`, `Match for third place` → `THIRD_PLACE`
- `Final`, `Finals` → `FINAL`

---

## Standardized Team and Country Names

Team names are standardized to prevent the same national team from being counted under multiple labels.

Examples include:

- `USA` → `United States`
- `Republic of Korea` → `South Korea`
- `Cape Verde` → `Cabo Verde`
- `DR Congo` → `Democratic Republic of the Congo`
- `West Germany` → `FR Germany`

Historical entities, such as `Soviet Union`, `Yugoslavia`, `Czechoslovakia`, `DR Germany` and `FR Germany`, may remain separate when required for historical consistency.

---

## Derived Fields

Several fields are calculated during the quality-control and analysis process.

### Unique Match Identifier

- **Description:** Concatenation of match attributes used to identify duplicate records.
- **Components:** Year, date, stage, stadium, city, teams, scores and win conditions.

### Valid Team

- **Description:** Indicates whether both participating teams are recognized by the normalization system.

### Winner

- **Description:** Identifies the winning team using the score and win-condition fields.
- **Possible values:** National team name or `MATCH NUL`.

### Win Condition Category

- **Description:** Standardized classification of how the match was decided.
- **Possible values:**
  - `WIN_BY_SCORE`
  - `WIN_BY_EXTRA_TIME`
  - `WIN_BY_PENALTY`
  - `WIN_BY_GOLDEN_GOAL`
  - `MATCH_NUL`

### Goals Conceded per Match

- **Description:** Total goals conceded divided by matches played.
- **Use:** Defensive performance analysis.

### Goal Difference per Match

- **Description:** Goals scored minus goals conceded, divided by matches played.
- **Use:** Comparison of net performance between teams.

---

## Data Limitations

- National teams and political entities have changed throughout World Cup history.
- Some historical names are preserved to maintain consistency with the source data.
- The number of matches varies significantly between teams.
- Penalty shootout goals are not added to the official match score.
- Extra-time goals are included in the recorded final score when present in the source.
- Data quality depends on the accuracy of the original dataset.
- If 2026 match results are simulated or projected, they must not be interpreted as confirmed 
