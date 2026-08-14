# Data Science Job Postings — SQL Analytics Project

Analyzing real-world data job postings to answer a simple question: **what skills should you actually learn to land a high-paying data role?**

## Overview

This project pulls a dataset of data science job postings, warehouses it, and runs SQL analysis to surface skill demand and pay trends — the kind of insight job seekers and career switchers can use to prioritize what to learn next.



## Architecture
![Project Architecture](https://raw.githubusercontent.com/bonsoul/Job_Posting_DE_Project/main/Images/DE%20Project.png)


**1. Data Warehouse**
Job postings data (company info, postings, skills, and skill-job mappings) is loaded into **DuckDB**, used here as a lightweight OLAP engine — fast columnar queries without spinning up a full server. The data was also mirrored into **PostgreSQL** for querying via pgAdmin/VS Code, using DuckDB's `postgres` extension to move data directly between the two.

**2. SQL Analytics**
Three core queries drive the analysis:

| Script | Purpose |
|---|---|
| `01_top_demanded_skills.sql` | Ranks skills by how often they appear across job postings — what's actually being asked for |
| `02_top_paying_skills.sql` | Ranks skills by average associated salary — what pays the most |
| `03_optimal_skills.sql` | Combines demand and pay to find the "sweet spot" — skills that are both in-demand *and* well-paid |

**3. Data Insights**
Output from the above: top demanded skills, high-paying skills, and optimal skills — the practical takeaways for anyone deciding what to learn or which roles to target.

## Data Model

The dataset follows a fact/dimension schema:

- `company_dim` — company details
- `job_postings_fact` — core fact table: one row per job posting (title, salary, location, remote flag, etc.), linked to `company_dim`
- `skills_dim` — master list of skills
- `skills_job_dim` — bridge table mapping postings to skills (many-to-many)

## Tools Used

- **DuckDB** — OLAP query engine, used to explore and transform the raw data
- **PostgreSQL** — relational store for the cleaned data, queried via pgAdmin and VS Code
- **SQL** — all analysis (aggregation, joins, window functions, percentiles)

## Key Questions Answered

- What are the most in-demand skills across data job postings?
- Which skills command the highest average salaries?
- Which skills strike the best balance of high demand *and* high pay — the "optimal skills" to prioritize?

## How to Run

1. Load the dataset into DuckDB (or attach the shared MotherDuck database).
2. Optionally mirror the tables into PostgreSQL for querying via pgAdmin/VS Code.
3. Run the SQL scripts in order:
   ```
   01_top_demanded_skills.sql
   02_top_paying_skills.sql
   03_optimal_skills.sql
   ```
4. Review the output for skill demand, pay, and the combined "optimal skills" ranking.

