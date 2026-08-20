# KPI Dictionary

## FIFA World Cup Analytics

## Purpose

This document describes the Key Performance Indicators used in the FIFA World Cup Analytics workbook.

KPIs are divided into five categories:

1. overview indicators;
2. historical team indicators;
3. offensive and defensive indicators;
4. normalized performance scores;
5. predictive indicators.

---

## 1. Overview KPIs

### Number of World Cup Editions

- **Category:** Overview
- **Definition:** Number of distinct World Cup years included in the match dataset.
- **Calculation:** Count of unique values in the `Year` field.
- **Source:** `DATA_CLEANED`
- **Format:** Integer
- **Interpretation:** Indicates the historical coverage of the project.

### Number of Matches

- **Category:** Overview
- **Definition:** Total number of unique matches included in the cleaned match dataset.
- **Calculation:** Count of cleaned match records.
- **Source:** `DATA_CLEANED`
- **Format:** Integer
- **Interpretation:** Indicates the total analytical volume.
- **Control:** The number of matches is reconciled by tournament edition.

### Number of Participating Teams

- **Category:** Overview
- **Definition:** Number of distinct national teams appearing as either the home or away team.
- **Calculation:** Unique count after combining the home-team and away-team columns.
- **Source:** `DATA_CLEANED`
- **Format:** Integer

### Total Goals

- **Category:** Overview
- **Definition:** Total number of goals scored in all analyzed matches.
- **Calculation:** Sum of home-team goals plus away-team goals.
- **Source:** `DATA_CLEANED`
- **Format:** Integer
- **Exclusion:** Penalty shootout kicks are not included.

### Average Goals per Match

- **Category:** Overview
- **Definition:** Average total number of goals scored during a match.
- **Calculation:** Total goals divided by total matches.
- **Source:** `DATA_CLEANED`
- **Format:** Decimal with two places
- **Interpretation:** Measures the general scoring intensity of the competition.

### Median Goals per Match

- **Category:** Overview
- **Definition:** Median of the total goals scored in individual matches.
- **Calculation:** Median of home goals plus away goals for each match.
- **Source:** `DATA_CLEANED`
- **Format:** Decimal
- **Interpretation:** Represents the typical match while reducing the influence of extreme scores.

### Number of Draws

- **Category:** Match result
- **Definition:** Number of matches ending without a winner according to the project's result rules.
- **Calculation:** Count of records classified as `MATCH NUL`.
- **Source:** `DATA_QUALITE`
- **Format:** Integer

### Penalty Shootouts

- **Category:** Match result
- **Definition:** Number of matches decided by a penalty shootout.
- **Calculation:** Count of matches classified as `WIN_BY_PENALTY`.
- **Source:** `DATA_QUALITE`
- **Format:** Integer

### Matches Decided by Golden Goal

- **Category:** Match result
- **Definition:** Number of matches decided under the golden-goal rule.
- **Calculation:** Count of matches classified as `WIN_BY_GOLDEN_GOAL`.
- **Source:** `DATA_QUALITE`
- **Format:** Integer

---

## 2. Historical Team KPIs

### Tournament Participations

- **Category:** Historical performance
- **Definition:** Number of World Cup editions in which a team played at least one match.
- **Calculation:** Count of edition years in which the team appears in a match.
- **Source:** `CALCULES`
- **Format:** Integer
- **Interpretation:** A high value indicates regular historical participation.

### Matches Played

- **Category:** Historical performance
- **Definition:** Total number of matches played by a national team.
- **Calculation:** Home appearances plus away appearances.
- **Source:** `DATA_CLEANED` and `CALCULES`
- **Format:** Integer

### Wins

- **Category:** Historical performance
- **Definition:** Total number of matches won by a national team under the project's winner-classification rules.
- **Calculation:** Count of matches for which the team is identified as the winner.
- **Source:** `DATA_QUALITE` and `CALCULES`
- **Format:** Integer
- **Note:** Penalty shootout victories may be treated as wins in the team record.

### Draws

- **Category:** Historical performance
- **Definition:** Number of matches in which the national team finished without a winner.
- **Calculation:** Count of `MATCH NUL` records involving the team.
- **Source:** `DATA_QUALITE` and `CALCULES`
- **Format:** Integer

### Defeats

- **Category:** Historical performance
- **Definition:** Number of matches lost by the national team.
- **Calculation:** Matches played minus wins minus draws.
- **Source:** `CALCULES`
- **Format:** Integer

### Win Rate

- **Category:** Historical performance
- **Definition:** Percentage of matches won by a national team.
- **Calculation:** Wins divided by matches played.
- **Source:** `CALCULES`
- **Format:** Percentage
- **Interpretation:** Higher values indicate a stronger historical win frequency.
- **Limitation:** The KPI must be interpreted together with the number of matches played.

### Highest Stage Reached

- **Category:** Tournament performance
- **Definition:** Best tournament stage reached by a national team.
- **Source:** `CALCULES`
- **Format:** Text
- **Possible values:**
  - `GROUP_STAGE`
  - `ROUND_OF_32`
  - `ROUND_OF_16`
  - `QUARTER_FINALS`
  - `SEMI_FINALS`
  - `THIRD_PLACE`
  - `FINAL`

### World Cup Titles

- **Category:** Tournament performance
- **Definition:** Number of World Cup finals won by a national team.
- **Calculation:** Count of finals in which the team is identified as the winner.
- **Source:** `CALCULES`
- **Format:** Integer

---

## 3. Offensive and Defensive KPIs

### Goals Scored

- **Category:** Offensive performance
- **Definition:** Total number of goals scored by a national team.
- **Calculation:** Home goals when playing at home plus away goals when playing away.
- **Source:** `DATA_CLEANED` and `CALCULES`
- **Format:** Integer

### Goals Conceded

- **Category:** Defensive performance
- **Definition:** Total number of goals conceded by a national team.
- **Calculation:** Away goals conceded when playing at home plus home goals conceded when playing away.
- **Source:** `DATA_CLEANED` and `CALCULES`
- **Format:** Integer

### Goals Scored per Match

- **Category:** Offensive performance
- **Definition:** Average goals scored by the team per match.
- **Calculation:** Goals scored divided by matches played.
- **Source:** `CALCULES`
- **Format:** Decimal with two places
- **Interpretation:** Higher values indicate stronger average offensive production.

### Goals Conceded per Match

- **Category:** Defensive performance
- **Definition:** Average goals conceded by the team per match.
- **Calculation:** Goals conceded divided by matches played.
- **Source:** `CALCULES`
- **Format:** Decimal with two places
- **Interpretation:** Lower values indicate stronger average defensive performance.

### Goal Difference

- **Category:** Global performance
- **Definition:** Difference between goals scored and goals conceded.
- **Calculation:** Goals scored minus goals conceded.
- **Source:** `CALCULES`
- **Format:** Integer

### Goal Difference per Match

- **Category:** Global performance
- **Definition:** Average net goal difference per match.
- **Calculation:** Goal difference divided by matches played.
- **Source:** `CALCULES`
- **Format:** Decimal with two places
- **Interpretation:** Positive values indicate that the team scores more goals than it concedes.

### Clean-Sheet Rate

- **Category:** Defensive performance
- **Definition:** Percentage of matches in which the team conceded no goals.
- **Calculation:** Matches with zero goals conceded divided by matches played.
- **Source:** `DATA_CLEANED` and `CALCULES`
- **Format:** Percentage
- **Interpretation:** Higher values indicate a greater ability to prevent opponents from scoring.

---

## 4. Normalized Performance Scores

### Offensive Score

- **Category:** Normalized score
- **Definition:** Synthetic score used to compare the offensive performance of national teams.
- **Scale:** 0 to 100
- **Main components:**
  - average goals scored per match;
  - median goals scored;
  - data-volume reliability adjustment.
- **Source:** `CALCULES`
- **Interpretation:** Higher values indicate a stronger and more reliable offensive record.
- **Limitation:** The score is specific to this project and is not an official FIFA rating.

### Defensive Score

- **Category:** Normalized score
- **Definition:** Synthetic score used to compare the defensive performance of national teams.
- **Scale:** 0 to 100
- **Main components:**
  - average goals conceded per match;
  - median goals conceded;
  - clean-sheet rate;
  - data-volume reliability adjustment.
- **Source:** `CALCULES`
- **Interpretation:** Higher values indicate stronger defensive performance.
- **Important:** A low goals-conceded average contributes positively to the score.

### Global Performance Score

- **Category:** Normalized score
- **Definition:** Combined measure of offensive and defensive performance.
- **Calculation principle:** Weighted average of the offensive and defensive scores.
- **Source:** `CALCULES`
- **Scale:** 0 to 100
- **Interpretation:** Provides a synthetic comparison of overall team strength.
- **Limitation:** This score is designed for comparative visualization and should not be interpreted as a match probability.

---

## 5. Recent Form KPIs

### Wins in the Last Five Matches

- **Category:** Recent form
- **Definition:** Number of matches won by a team among its five most recent available matches.
- **Format:** `x/5`
- **Special rule:** If fewer than five matches are available, the denominator is the number of available matches.
- **Examples:**
  - `4/5`
  - `2/3`
  - `0/1`
- **Source:** `DATA_CLEANED`
- **Interpretation:** Higher values indicate stronger recent form.
- **Limitation:** The KPI does not account for opponent strength.

### Form Coefficient

- **Category:** Predictive adjustment
- **Definition:** Limited coefficient derived from the recent win ratio.
- **Minimum:** `0.90`
- **Maximum:** `1.10`
- **Calculation principle:** `0.90 + 0.20 × recent win ratio`
- **Interpretation:** Recent form modifies expected goals by a maximum of approximately 10% in either direction.

---

## 6. Predictive KPIs

### Expected Goals for Team A

- **Category:** Predictive
- **Definition:** Estimated average number of goals that team A may score against team B.
- **Symbol:** `λA`
- **Main components:**
  - adjusted attacking performance of team A;
  - adjusted defensive performance of team B;
  - strength coefficient;
  - recent-form coefficient.
- **Source:** `DASHBOARD` predictive model
- **Format:** Decimal with two places

### Expected Goals for Team B

- **Category:** Predictive
- **Definition:** Estimated average number of goals that team B may score against team A.
- **Symbol:** `λB`
- **Source:** `DASHBOARD` predictive model
- **Format:** Decimal with two places

### Team A Win Probability

- **Category:** Predictive
- **Definition:** Sum of the probabilities of all calculated score combinations in which team A scores more goals than team B.
- **Calculation:** Poisson score matrix.
- **Format:** Percentage

### Draw Probability

- **Category:** Predictive
- **Definition:** Sum of the probabilities of all calculated score combinations in which both teams score the same number of goals.
- **Calculation:** Diagonal of the Poisson score matrix.
- **Format:** Percentage

### Team B Win Probability

- **Category:** Predictive
- **Definition:** Sum of the probabilities of all calculated score combinations in which team B scores more goals than team A.
- **Calculation:** Poisson score matrix.
- **Format:** Percentage

### Probability Control

- **Category:** Technical control
- **Definition:** Sum of team A win probability, draw probability and team B win probability.
- **Expected result:** Approximately 100%
- **Note:** A slight difference may remain because the model limits the score matrix to a defined maximum number of goals.

### Most Likely Score

- **Category:** Predictive
- **Definition:** Exact score combination with the highest individual probability.
- **Format:** `Team A goals - Team B goals`
- **Example:** `2 - 1`
- **Important:** The most likely exact score is not necessarily the same as the most likely overall match outcome.

### Most Likely Score Probability

- **Category:** Predictive
- **Definition:** Individual probability associated with the most likely exact score.
- **Format:** Percentage

### Confidence Index

- **Category:** Predictive quality
- **Definition:** Indicator describing the reliability of the probability model according to the historical match volume available for both teams.
- **Possible values:**
  - `Low`
  - `Medium`
  - `High`
- **Interpretation:** A high confidence level indicates that both teams have a substantial number of historical match records.
- **Limitation:** A high confidence level does not guarantee that the prediction is correct.

---

## General Interpretation Rules

- A high score does not guarantee a future victory.
- A small sample size can create unstable averages.
- Historical performance and recent form measure different dimensions.
- The most likely exact score can have a relatively low probability.
- Match probabilities should always be read together with the confidence index.
- Predictive KPIs are indicative and must not be used as betting advice.
