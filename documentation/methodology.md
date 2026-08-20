# Methodology

## FIFA World Cup Analytics

## 1. Project Approach

The project follows a complete Business Intelligence workflow:

`Business objective → Raw data → Data quality → Data cleaning → Analysis → KPIs → Dashboard → Documentation`

The objective is to preserve the traceability of the data while producing a reliable and understandable analytical output.

---

## 2. Business Questions

The project was designed to answer questions such as:

- How has the FIFA World Cup evolved since 1930?
- Which national teams have achieved the strongest historical results?
- Which teams have the strongest offensive and defensive profiles?
- Which teams have participated most frequently?
- Which teams have reached the most advanced tournament stages?
- How have scoring levels evolved across tournament editions?
- How can two national teams be compared using common performance indicators?
- What indicative outcome is suggested by their historical statistics and recent form?

---

## 3. Source Data Preservation

The original source data is stored in the `DATA_BRUT` worksheet.

This worksheet is preserved to:

- maintain a reference copy of the imported data;
- compare raw and cleaned values;
- document all transformations;
- ensure that the cleaning process is reproducible;
- avoid modifying the source directly.

No analytical dashboard should rely directly on the raw data when a cleaned equivalent is available.

---

## 4. Data Quality Assessment

The data-quality process is documented in the `DATA_QUALITE` worksheet.

### 4.1 Duplicate Detection

A unique match identifier is created by combining:

- tournament year;
- match date;
- tournament stage;
- stadium;
- host city;
- home team;
- home score;
- away score;
- away team;
- win conditions.

Records with identical identifiers are flagged as duplicates.

Confirmed duplicate match records are removed from the analytical dataset.

### 4.2 Country and Team Name Validation

Team and country names are compared with reference lists and correction mapping tables.

The objective is to prevent one team from being counted under several names.

Examples include:

- `USA` → `United States`
- `Republic of Korea` → `South Korea`
- `Cape Verde` → `Cabo Verde`
- `DR Congo` → `Democratic Republic of the Congo`
- `West Germany` → `FR Germany`

Historical entities may remain distinct when merging them would distort the historical analysis.

### 4.3 Character-Encoding Control

The project checks text fields for incorrectly encoded characters.

Fields controlled include:

- stadium names;
- city names;
- player names;
- goalkeeper names;
- club names.

Examples of corrected values include accented stadium and city names.

### 4.4 Numerical Data Validation

Fields expected to contain numerical values are checked and converted where required.

Examples include:

- tournament year;
- home goals;
- away goals;
- player age;
- shirt number;
- kick number.

### 4.5 Tournament Stage Normalization

Source tournament stages contain several naming conventions.

Equivalent source values are mapped to standardized categories:

- `GROUP_STAGE`
- `ROUND_OF_32`
- `ROUND_OF_16`
- `QUARTER_FINALS`
- `SEMI_FINALS`
- `THIRD_PLACE`
- `FINAL`

This standardization allows tournament-stage comparisons across different editions.

### 4.6 Score and Winner Verification

The winner is determined using:

1. home and away goals;
2. extra-time information;
3. penalty-shootout information;
4. golden-goal information.

Possible result categories include:

- `WIN_BY_SCORE`
- `WIN_BY_EXTRA_TIME`
- `WIN_BY_PENALTY`
- `WIN_BY_GOLDEN_GOAL`
- `MATCH_NUL`

Penalty shootout kicks are not added to the official match score.

### 4.7 Match Count Reconciliation

The number of matches is checked by tournament edition.

The cleaned count is compared with the expected number of matches. Differences are investigated before the data is used in the final dashboard.

---

## 5. Cleaned Dataset

The `DATA_CLEANED` worksheet contains the standardized data used by the analytical model.

The main transformations include:

- removal of confirmed duplicates;
- correction of character-encoding problems;
- standardization of team and country names;
- conversion of numerical fields;
- standardization of tournament stages;
- standardization of missing win conditions;
- preservation of historical information.

The cleaned match dataset is the primary source for the dashboard and team-level calculations.

---

## 6. Team-Level Analysis

Team-level statistics are calculated by combining home-team and away-team records.

For each national team, the project calculates:

- tournament participations;
- matches played;
- wins;
- draws;
- defeats;
- goals scored;
- goals conceded;
- goals scored per match;
- goals conceded per match;
- goal difference;
- goal difference per match;
- clean-sheet rate;
- highest tournament stage reached;
- World Cup titles.

### Goals Scored

Goals scored are calculated as:

- home-team goals when the team plays at home;
- away-team goals when the team plays away.

### Goals Conceded

Goals conceded are calculated as:

- away-team goals when the team plays at home;
- home-team goals when the team plays away.

### Win Rate

The win rate is calculated as:

`Wins ÷ Matches played`

The number of matches must always be considered when comparing win rates, because a high percentage based on a small sample is less reliable.

---

## 7. Offensive Score

The offensive score is a normalized indicator on a scale from 0 to 100.

The score is intended to summarize:

- average goals scored per match;
- consistency of goals scored;
- the reliability of the available match volume.

The average is used as the main offensive input because it reflects total scoring production.

The median is used as a secondary indicator because it reduces the influence of unusually high scores.

A reliability adjustment is applied to avoid treating a team with only a few matches as being as statistically reliable as a team with a long World Cup history.

The offensive score is a project-specific comparison indicator and is not an official FIFA rating.

---

## 8. Defensive Score

The defensive score is also normalized on a scale from 0 to 100.

The score is intended to summarize:

- average goals conceded per match;
- consistency of goals conceded;
- clean-sheet performance;
- the reliability of the available match volume.

Because conceding fewer goals represents stronger defensive performance, defensive inputs are inverted before normalization.

A higher defensive score therefore represents a stronger defensive record.

---

## 9. Global Performance Score

The global score combines the offensive and defensive scores.

The purpose of this score is to provide a concise comparison between national teams.

The global score is used for descriptive comparison and strength adjustment. It is not interpreted directly as a win probability.

---

## 10. Recent Form

Recent form is based on the team's five most recent matches.

The model calculates the number of wins during this period.

If a team has fewer than five matches in the dataset, all available matches are used.

Examples include:

- `5/5`
- `3/5`
- `2/3`
- `0/1`

A limited form coefficient is then calculated. The coefficient ranges approximately from `0.90` to `1.10`.

This limitation prevents five recent matches from having more influence than the team's full historical record.

---

## 11. Expected Goals Model

The `VERSUS` section estimates the expected goals for two selected national teams.

The expected-goals values are represented by:

- `λA` for team A;
- `λB` for team B.

The model uses:

- adjusted goals scored per match;
- adjusted goals conceded per match;
- historical data reliability;
- relative team strength;
- recent form.

The expected goals represent the estimated average scoring intensity for the selected match scenario.

The model does not use penalty shootout kicks as match goals.

---

## 12. Reliability Adjustment

The number of available matches varies significantly by national team.

A reliability coefficient is therefore applied to reduce the effect of extreme statistics calculated from small samples.

The principle is:

`Adjusted statistic = Team statistic × reliability + competition average × (1 - reliability)`

As the number of matches increases, the adjusted statistic moves closer to the team's observed statistic.

When the number of matches is small, the statistic remains closer to the overall competition average.

---

## 13. Strength Adjustment

A limited strength coefficient is created from the difference between the two teams' global scores.

The coefficient is capped to prevent unrealistic expected-goal values.

The global score therefore adjusts the expected goals but does not replace the goals-scored and goals-conceded statistics.

This ensures that the probability model remains primarily performance-based.

---

## 14. Poisson Probability Model

The model uses a Poisson distribution to estimate the probability that each team scores a given number of goals.

Score probabilities are calculated from `0-0` to `8-8`.

For each score combination, the model calculates:

`Probability of Team A goals × Probability of Team B goals`

### Team A Win Probability

The probability of a team A win is the sum of all score combinations where:

`Team A goals > Team B goals`

### Draw Probability

The draw probability is the sum of all score combinations where:

`Team A goals = Team B goals`

### Team B Win Probability

The probability of a team B win is the sum of all score combinations where:

`Team A goals < Team B goals`

### Probability Control

The three outcome probabilities should total approximately 100%.

A small difference may remain because the matrix is limited to a maximum of eight goals per team.

---

## 15. Most Likely Score

The most likely score is the individual score combination with the highest probability in the Poisson matrix.

This score must be distinguished from the most likely overall outcome.

For example, the overall probability of a team A victory may be 55%, while the single most likely score may still be a draw such as `1-1`.

This occurs because team A's win probability is distributed across several different winning scores.

---

## 16. Confidence Index

The confidence index describes the quantity of historical information available for the selected teams.

The model uses three levels:

- **Low:** limited historical match data;
- **Medium:** moderate historical match data;
- **High:** substantial historical match data for both teams.

The confidence index does not measure whether a prediction will be correct. It only indicates the relative reliability of the statistical inputs.

---

## 17. Dashboard Design

The dashboard is designed to provide several levels of analysis.

### Overview

Provides the principal tournament KPIs.

### Historical Evolution

Shows how the competition has evolved by tournament edition.

### Historical Performance

Compares the performance and achievements of national teams.

### Offensive and Defensive Rankings

Ranks teams according to normalized performance indicators.

### Match-End Analysis

Examines draws, extra time, penalty shootouts and golden-goal decisions.

### VERSUS

Allows users to compare two selected teams and display an indicative match scenario.

Technical calculations are kept separate from the user-facing dashboard whenever possible.

---

## 18. Validation

The project includes several validation controls:

- duplicate-record verification;
- team-name reconciliation;
- tournament-stage mapping;
- score verification;
- winner verification;
- match-count reconciliation;
- probability-total control;
- error-value checks.

The Poisson probabilities are controlled by verifying that the sum of team A wins, draws and team B wins is close to 100%.

---

## 19. Limitations

The project has several limitations.

### Historical Entities

Countries and national teams have changed over time. Historical teams may not be directly comparable with current national teams.

### Unequal Sample Sizes

Some teams have played more than 100 World Cup matches, while others have played only a few.

### Opponent Strength

The current model does not fully adjust each performance according to the strength of the opponents faced.

### Match Location

Home advantage, host-country advantage and travel conditions are not fully integrated.

### Squad Information

The model does not include:

- player injuries;
- squad selections;
- tactical changes;
- player form;
- coaching changes.

### Poisson Assumptions

The Poisson model assumes that scoring events can be modeled independently. Real football matches may not fully respect this assumption.

### 2026 Data

If the 2026 match data is simulated or projected, the results must be interpreted as scenario data rather than confirmed historical results.

---

## 20. Future Improvements

Possible future developments include:

- rebuilding the data-cleaning process with Power Query;
- creating a relational data model;
- reproducing the project in SQL;
- rebuilding the dashboard in Power BI;
- creating DAX measures;
- adjusting for opponent strength;
- separating historical and projected data;
- adding home and away performance;
- incorporating tournament-stage weighting;
- adding head-to-head analysis;
- backtesting predictions against historical matches;
- comparing predicted and observed results;
- integrating Microsoft Fabric.

---

## 21. Reproducibility

To reproduce the analysis:

1. import the original source datasets;
2. preserve them in the raw-data layer;
3. run the documented quality controls;
4. apply the mapping tables;
5. remove confirmed duplicate records;
6. create the cleaned match dataset;
7. calculate the team-level indicators;
8. calculate the normalized scores;
9. build the dashboard;
10. validate the probability totals and key counts.

A recent version of Microsoft Excel is recommended because the project uses dynamic-array functions and advanced formulas.
