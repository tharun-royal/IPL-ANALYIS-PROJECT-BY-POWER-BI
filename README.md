
# IPL Data Analysis Dashboard (2008-2024) | Power BI

An interactive Power BI dashboard that analyzes every Indian Premier League season from 2008 to 2024. It covers match results, team performance, toss impact, batting and bowling records, and venue trends.

## Project Objective

- Understand how IPL scoring and match outcomes have changed over the seasons
- Identify top performing teams, batters and bowlers
- Check whether winning the toss helps win the match
- Find which venues host the most matches and favor batting or bowling

## Dataset

- **Source:** [IPL Complete Dataset (2008-2024) on Kaggle](https://www.kaggle.com/datasets/patrickb1912/ipl-complete-dataset-20082020)
- **Original data:** Cricsheet

| File | Description | Size |
|------|-------------|------|
| `matches.csv` | One row per match: season, teams, venue, toss, winner, player of the match | 1,095 rows, 20 columns |
| `deliveries.csv` | One row per ball: batter, bowler, runs, wickets, extras | 260,920 rows, 17 columns |

## Tools Used

- **Power BI Desktop** for data modeling and visualization
- **Power Query** for data cleaning
- **DAX** for calculated measures

## Data Cleaning (Power Query)

- Set correct data types (date, whole numbers, text)
- Standardized team names that changed over time:
  - Delhi Daredevils → Delhi Capitals
  - Royal Challengers Bangalore → Royal Challengers Bengaluru
  - Kings XI Punjab → Punjab Kings
- Handled null values in `winner` and `city`
- Removed duplicate rows

## Data Model

`matches[id]` → `deliveries[match_id]` (one-to-many, single direction)

## Key DAX Measures

```DAX
Total Matches = COUNTROWS(matches)

Total Runs = SUM(deliveries[total_runs])

Total Wickets = CALCULATE(COUNTROWS(deliveries), deliveries[is_wicket] = 1)

Total Sixes = CALCULATE(COUNTROWS(deliveries), deliveries[batsman_runs] = 6)

Total Fours = CALCULATE(COUNTROWS(deliveries), deliveries[batsman_runs] = 4)

Batter Runs = SUM(deliveries[batsman_runs])

Balls Faced = CALCULATE(COUNTROWS(deliveries), deliveries[extras_type] <> "wides")

Strike Rate = DIVIDE([Batter Runs], [Balls Faced]) * 100

Toss Win Match Win % =
DIVIDE(
    CALCULATE(COUNTROWS(matches), matches[toss_winner] = matches[winner]),
    [Total Matches]
) * 100
```

## Dashboard Pages

### 1. Season Overview
- KPI cards: Total Matches, Total Runs, Total Sixes, Total Fours
- Slicers: Season, Team
- Line chart: runs per season
- Bar chart: most wins by team
- Donut chart: toss decision (bat vs field)
- Bar chart: top 10 venues by matches played

### 2. Batting and Bowling
- Top 10 run scorers
- Top 10 wicket takers
- Batter table: runs, balls, strike rate, 4s, 6s
- Scatter chart: strike rate vs runs

### 3. Team and Match Insights
- Top 10 Player of the Match winners
- Matrix: team wins by season
- Toss win vs match win percentage
- Win by runs vs win by wickets
- Average first-innings score by venue

## Key Insights

> Replace these with your own findings after building the dashboard.

- Team with the most wins: _your finding_
- Impact of the toss on the result: _your finding_
- Top run scorer and top wicket taker: _your finding_
- Venue that favors batting: _your finding_
- Scoring trend over seasons: _your finding_

## Screenshots

Add your screenshots to a `screenshots` folder and link them here:

```
![Season Overview](screenshots/page1.png)
![Batting and Bowling](screenshots/page2.png)
![Team Insights](screenshots/page3.png)
```

## How to Run

1. Download the dataset from the Kaggle link above
2. Clone or download this repository
3. Open `IPL_Analysis.pbix` in Power BI Desktop
4. If prompted, update the file paths: **Home → Transform data → Data source settings**
5. Click **Refresh**

## Repository Structure

```
IPL-Power-BI/
├── IPL_Analysis.pbix
├── data/
│   ├── matches.csv
│   └── deliveries.csv
├── screenshots/
└── README.md
```

## Author

**Your Name**
[LinkedIn](https://linkedin.com/in/your-profile) | [GitHub](https://github.com/your-username)
