2025 MLB Regular Season Analytics
An end-to-end data analytics project analyzing the 2025 MLB regular season using a modern data stack. Raw baseball data is loaded into Snowflake, transformed and modeled with dbt, and visualized in Power BI.

Project Overview
This project explores team and player performance across the 2025 MLB regular season. The goal is to identify trends in offensive and pitching efficiency, team win drivers, and player standout metrics — while demonstrating a production-style analytics workflow.

Tools & Stack
LayerToolData WarehouseSnowflakeTransformationdbt CoreVisualizationPower BIVersion ControlGitHubData SourceBaseball Reference / Retrosheet / MLB Stats API

Data Sources

MLB Stats API (stats.mlb.com) — play-by-play, player stats, standings
Baseball Reference — season batting, pitching, and fielding tables
Retrosheet — historical game logs for 2025 regular season


Project Structure
├── data/
│   └── raw/                  # Raw CSV files loaded into Snowflake
├── dbt/
│   ├── models/
│   │   ├── staging/          # Clean, renamed source tables (stg_*)
│   │   ├── intermediate/     # Joined and reshaped models (int_*)
│   │   └── marts/            # Final analytics-ready tables (fct_*, dim_*)
│   ├── tests/                # dbt data quality tests
│   └── dbt_project.yml
├── dashboards/
│   └── mlb_2025.pbix         # Power BI dashboard file
└── README.md

dbt Models
Staging

stg_batting — cleaned 2025 batting stats per player
stg_pitching — cleaned 2025 pitching stats per player
stg_standings — team win/loss records by week

Intermediate

int_team_offense — aggregated team-level offensive metrics
int_starting_pitchers — ERA, WHIP, K/9 for qualified starters

Marts

fct_team_performance — weekly team win % vs run differential
dim_players — player dimension with position, team, and handedness


Key Analysis Questions

Which teams had the highest run differential and did it correlate with playoff position?
Who were the most efficient starting pitchers by ERA+ and innings pitched?
Which hitters led in WAR relative to salary tier?
How did team batting average with runners in scoring position (RISP) rank against win totals?


Data Quality
All dbt models include the following tests:

not_null on all primary keys
unique on player and game IDs
accepted_values on position and handedness fields
Custom test: season stat totals reconcile to official MLB totals


How to Run
Prerequisites

Snowflake account (free trial at snowflake.com)
dbt Core installed (pip install dbt-snowflake)
Python 3.8+

Setup
bash# Clone the repo
git clone https://github.com/yourusername/mlb-2025-analytics.git
cd mlb-2025-analytics

# Install dbt dependencies
pip install dbt-snowflake

# Configure your Snowflake connection
cp profiles_template.yml ~/.dbt/profiles.yml
# Edit profiles.yml with your Snowflake credentials

# Run dbt models
cd dbt
dbt deps
dbt run
dbt test

Dashboard Preview
The Power BI dashboard covers four pages:

League Overview — standings, run differential, pythagorean win %
Pitching Leaders — ERA, WHIP, K/9, FIP for qualified starters
Hitting Leaders — WAR, OPS+, wRC+ leaderboard
Team Deep Dive — filterable team-level breakdown by month


Status
MilestoneStatusSnowflake environment setup✅ CompleteRaw data loaded✅ CompleteStaging models🔄 In progressIntermediate models🔄 In progressMart models⬜ Not startedPower BI dashboard⬜ Not startedDocumentation🔄 In progress
