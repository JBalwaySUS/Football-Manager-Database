# Football Manager Database System

A relational database system and match simulator for football management. The repository contains a 22-table SQL database schema, an interactive Python CLI for database CRUD operations, and a match simulator that generates fixture results and player statistics based on team ratings.

*Developed as a team project for the Database and Database Applications (DNA) course.*

## Features

* **Database Schema (22 Tables)**: Covers core entities including clubs, players, managers, stadiums, tactics, leagues, contracts, injuries, and match performances.
* **Interactive Python CLI (`python/src/main.py`)**: Terminal interface to add, update, delete, and view database records across all tables. Includes name searching and input validation.
* **Match & Season Simulator (`python/simulator/simulator.py`)**:
  * Schedules round-robin league matches for a season.
  * Simulates match scores using team overall ratings and Gaussian distribution.
  * Generates player performance stats (goals, assists, pass accuracy, distance covered, ratings).
  * Evaluates manager tactical matchups.
  * Updates league tables, points, and leaderboards (Top Scorers, Top Assists, Clean Sheets).
* **Sample Data (`creator.sql`, `football.sql`)**: SQL scripts with table definitions and pre-populated data for Premier League and EFL Championship teams.

## Database Schema Overview

The database contains 22 tables grouped into four main areas:

| Category | Table Name | Description |
| :--- | :--- | :--- |
| **Core Entities** | `clubs` | Club information, foundation date, budget, prestige, stadium, manager |
| | `players` | Player attributes, market value, height, weight, overall rating, club, mentor |
| | `managers` | Experience, salary, preferred tactic |
| | `stadiums` | Capacity, city, ticket fare |
| | `tactics` | Tactical instructions, formation, playstyle |
| | `leagues` | Season year, upper/lower leagues, champions, top performers |
| | `leaguedetails` | Nation, team count, promotion and relegation tiers |
| **Matches & Standings** | `matchx` | Fixtures, dates, scores, attendance, teams, stadium, league |
| | `playermatchperformance` | Stats per match: goals, assists, pass accuracy, distance, ratings |
| | `managermatchperformance` | Manager rating per match and tactical matchups |
| | `playsin` | Links clubs to leagues and tracks total points |
| **Contracts & Status** | `contracts` | Contract dates, salary, validity, player-club link |
| | `injuryrecord` | Player injury logs, severity, recurrence rate |
| | `recoveryprediction` | Days to recovery based on injury severity and recurrence rate |
| | `youthplayer` | Youth academy join dates, levels, graduation targets |
| | `captain` | Captain win rates and bonuses |
| | `loanplayer` | Loan start/end dates and original club |
| **Attributes & Details** | `playernationality` | Player nationalities |
| | `playerlanguagespoken` | Languages spoken by players |
| | `playerpositionsplayed` | Positions played (GK, ST, CM, CB, etc.) |
| | `managernationality` | Manager nationalities |
| | `managerachievements` | Manager trophies and awards |

## Repository Structure

```text
Football-Manager-Database/
├── creator.sql                 # SQL schema definition and sample data
├── football.sql                # Full database dump
├── README.md                   # Project documentation
└── python/
    ├── simulator/
    │   └── simulator.py        # Match simulator script
    └── src/
        ├── main.py             # Main CLI entry point
        ├── clubs.py            # Club operations
        ├── players.py          # Player operations
        ├── managers.py         # Manager operations
        ├── stadium.py          # Stadium operations
        ├── tactic.py           # Tactic operations
        ├── leagues.py          # League operations
        ├── leaguedetails.py    # League details operations
        ├── matchx.py           # Match operations
        ├── contracts.py        # Contract operations
        ├── injuryrecord.py     # Injury record operations
        ├── recoveryprediction.py # Recovery prediction operations
        ├── playermatchperformance.py # Player match performance operations
        ├── managermatchperformance.py# Manager match performance operations
        ├── managerachievements.py # Manager achievements operations
        ├── captain.py          # Captain stats operations
        ├── loanplayer.py       # Loan player operations
        ├── youthplayer.py      # Youth player operations
        ├── playsin.py          # League participation operations
        ├── playernationality.py# Player nationality operations
        ├── playerlanguagespoken.py# Spoken languages operations
        ├── playerpositionsplayed.py# Player positions operations
        └── managernationality.py # Manager nationality operations
```

## Prerequisites

* Python 3.8+
* MySQL 8.0+ or MariaDB 10.4+
* `pymysql` library

Install dependencies:
```bash
pip install pymysql
```

## Setup & Running

1. **Import Database**:
   Import `creator.sql` or `football.sql` into MySQL:
   ```bash
   mysql -u root -p < creator.sql
   ```

2. **Configure Database Credentials**:
   Update host, user, password, and port settings in `python/src/main.py` and `python/simulator/simulator.py`:
   ```python
   con = pymysql.connect(
       host='localhost',
       port=3306,
       user="root",
       password="YOUR_PASSWORD",
       db='Football',
       cursorclass=pymysql.cursors.DictCursor
   )
   ```

3. **Run the CLI Interface**:
   ```bash
   python python/src/main.py
   ```

4. **Run the Simulator**:
   ```bash
   python python/simulator/simulator.py
   ```
