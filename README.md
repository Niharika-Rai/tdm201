# TDM 201 — Data Engineering & Analytics Portfolio

**Niharika Rai** · Purdue University · The Data Mine (TDM 201, Fall 2025)

This repository holds 11 hands-on data projects I completed in **TDM 201**, the second-year seminar of [The Data Mine](https://datamine.purdue.edu/) at Purdue University. TDM 201 is required for The Data Mine **Corporate Partners Program**, and this was my second year in The Data Mine after TDM 102. I took the 1-credit-hour version of the course.

Over the semester I worked across the whole data stack. I started with **command-line processing of multi-gigabyte files** on a high-performance computing cluster, then moved to **relational databases and advanced SQL**, and finished with **NoSQL (MongoDB) document modeling, aggregation pipelines, and query performance tuning** in Python.

All work ran on **Purdue's Anvil supercomputer** (an NSF-funded HPC cluster) against real-world datasets, using Jupyter notebooks.

---

## At a Glance

| | |
|---|---|
| **Projects** | 11 Jupyter notebooks, 55 graded questions in total |
| **Languages** | Bash, awk, SQL (SQLite), Python |
| **Libraries & tools** | pandas, PyMongo, MongoDB, SQLite3, ipython-sql (`%%sql`), Jupyter, GNU coreutils, regex |
| **Environment** | Purdue Anvil HPC cluster (Linux, `$HOME` and `$SCRATCH` storage) |
| **Data scale** | Files up to 1.9 GB, several million rows per file, a 27-table relational database, and a 45,000+ document NoSQL collection |
| **Domains** | Transportation, e-commerce, food delivery, music, film/TV, sports analytics, retail |

---

## Technical Skills Demonstrated

### Data Wrangling on the Command Line
- Navigated and managed files on a shared Linux HPC filesystem (`cd`, `ls -la`, `cp -r`, `mv`, `rm -r`, `mkdir`, `touch`, quotas and scratch storage).
- Profiled large files without loading them into memory, using `head`, `tail`, `wc`, `ls -lh`, and `awk '{print NF}'`.
- Built multi-stage **Unix pipelines** (`grep | cut | sort | uniq -c | sort -nr | head`) to answer business questions from raw CSV, pipe-delimited, and TSV data.
- Wrote **regular expressions** with `grep -E`, `grep -P`, anchors (`^`, `$`), whole-word matching, inverted matches, and recursive search across directories.
- Wrote **awk programs** with conditional filters, running totals, **associative arrays** for group-by aggregation, ternary expressions to handle missing values, `printf` formatting, and `BEGIN`/`END` blocks that produce formatted reports.

### Relational Databases & SQL
- Explored an unfamiliar 27-table schema (the Lahman Baseball Database) through `sqlite_master`.
- Wrote filtering, sorting, and aggregation queries using `WHERE`, `AND`/`OR`, `LIKE`, `BETWEEN`, `ORDER BY`, `GROUP BY`, `HAVING`, `COUNT`, `SUM`, `AVG`, and `MAX`.
- Joined three tables at once on **composite keys** (`teamID` + `yearID`), and compared **INNER vs. LEFT JOIN** results to check data integrity.
- Structured complex logic with **Common Table Expressions (CTEs)**, including several CTEs joined together in one query.
- Practiced full **DDL and DML** work: `CREATE TABLE` with `PRIMARY KEY` and `NOT NULL` constraints, `INSERT ... SELECT` with a **correlated subquery**, `ALTER TABLE ADD/DROP COLUMN`, `DELETE`, and `DROP TABLE`.
- Built database automation with **triggers** (`AFTER INSERT ... FOR EACH ROW`) and reusable **views**.
- Managed **transactions** with `BEGIN`, `SAVEPOINT`, `ROLLBACK TO`, `RELEASE`, and `COMMIT`, and handled constraint violations (`UNIQUE`, `INSERT OR IGNORE`).
- Debugged real-world data problems, such as a UTF-8 decoding error in player names and differences between SQL dialects (SQLite has no `TRUNCATE`).

### NoSQL / MongoDB with Python
- Built an **ETL step** that loads CSV (pandas) and nested JSON data into MongoDB collections with PyMongo (45,466 movie documents).
- Queried documents with comparison, logical, and regex operators, **dot notation** for nested fields, and **`$elemMatch`** for arrays of sub-documents.
- Built **aggregation pipelines** using `$match`, `$group`, `$sort`, `$limit`, `$addFields`, `$substr`, `$switch` (value bucketing), `$unwind`, and **`$lookup`** (joins across collections).
- Performed CRUD operations at scale with `update_one`, `update_many`, and `delete_many`.
- Tuned performance with **single-field, compound, multikey, nested-field, unique, and text indexes**, and checked their effect with `explain()` execution statistics and `collStats`.
- Connected MongoDB to **pandas** for analysis: flattened nested documents, used `explode`, `groupby().agg()`, `value_counts`, `merge`, datetime parsing, and `unstack` pivot tables.
- Wrote a recursive Python helper that pulls execution-time metrics out of MongoDB's nested `explain` output, which is structured differently across server versions.

### Professional Practices
- Documented my reasoning for each question in plain English, next to the code that produced each answer.
- Kept a transparent record of the external resources I used (instructor videos, documentation, discussion boards, and AI assistants) at the start of every project, in line with the course's academic-integrity policy.
- Validated results before reporting them: I counted rows and checked for nulls after joins, re-queried tables after inserts and deletes, and checked filtered output against the source data.

---

## Project Breakdown

| # | Notebook | Focus | Dataset(s) | Key Techniques |
|---|---|---|---|---|
| 1 | [Project 1](Niharika_Rai_project1.ipynb) | Profiling large files in Bash | Bay Area Bike Share (1.9 GB station-status file), Bay Wheels, FEC election data | `head`, `awk -F`, `cut`, `grep`, counting rows that match a condition |
| 2 | [Project 2](Niharika_Rai_project2.ipynb) | Linux filesystem and HPC storage | Zillow housing, Breyers ice-cream reviews | Relative and absolute paths, `wc`, `cp -r`, `mv`, `$HOME` vs `$SCRATCH`, quotas |
| 3 | [Project 3](Niharika_Rai_project3.ipynb) | Text search and Unix pipelines | Million Song tracks, Amazon Fine Food Reviews (~568K reviews), IMDb, Rotten Tomatoes | `grep` flags, recursive search, regex, `tr`, `sort \| uniq -c \| sort -nr` |
| 4 | [Project 4](Niharika_Rai_project4.ipynb) | Analytics with awk | Restaurant / food-delivery orders, customers, vendors (1M+ rows) | Associative arrays, group-by aggregation, handling missing values, formatted reports |
| 5 | [Project 5](Niharika_Rai_project5.ipynb) | SQL fundamentals | Lahman Baseball Database (SQLite) | Schema discovery, `WHERE`, `ORDER BY`, `GROUP BY`, `COUNT`, encoding issues |
| 6 | [Project 6](Niharika_Rai_project6.ipynb) | Joins and CTEs | Lahman: People, Salaries, Batting, CollegePlaying | `JOIN`, `WITH` CTEs, career statistics, comparing schools |
| 7 | [Project 7](Niharika_Rai_project7.ipynb) | Advanced aggregation | Lahman: Salaries, People, Teams | Three-table joins, composite keys, INNER vs LEFT JOIN, `HAVING`, multiple CTEs |
| 8 | [Project 8](Niharika_Rai_project8.ipynb) | DDL / DML and schema changes | Local copy of the Lahman database | `CREATE`/`ALTER`/`DROP`, `INSERT ... SELECT`, correlated subqueries, database backup |
| 9 | [Project 9](Niharika_Rai_project9.ipynb) | Triggers, views, transactions | Local copy of the Lahman database | `CREATE TRIGGER`, `CREATE VIEW`, `SAVEPOINT`/`ROLLBACK`, integrity constraints |
| 10 | [Project 10](Niharika_Rai_mongodb_project10.ipynb) | Intro to MongoDB | MovieLens movie metadata (45,466 movies) | CSV → MongoDB ingestion, find/sort/limit, aggregation pipelines, CRUD |
| 11 | [Project 11](Niharika_Rai_mongodb_project11.ipynb) | Advanced MongoDB and performance | E-commerce dataset (products, customers, orders) | `$elemMatch`, `$unwind`, `$lookup`, pandas integration, indexing, `explain()` |

---

## Highlights

### 1. Analyzing a 1M+ row delivery dataset with awk (Project 4)
Using only awk, I found the most frequent customer (262 orders), the vendor most often marked as a favorite, and what share of a vendor's orders were discounted. I also produced a formatted "Best Customers" report straight from the command line.

```bash
awk -F, -v vendor="148" '
NR>1 && $22 == vendor { total++; if ($7 > 0) discounted++ }
END {
    pct = (discounted / total) * 100
    printf "Vendor: %s\nTotal Orders: %d\nDiscounted Orders: %d\nPercentage Discounted: %.2f%%\n",
           vendor, total, discounted, pct
}' orders.csv
# Vendor: 148 | Total Orders: 1078 | Discounted Orders: 183 | Percentage Discounted: 16.98%
```

### 2. Checking join integrity across three tables (Project 7)
I joined `Salaries`, `People`, and `Teams` on a composite key. Then I showed that INNER and LEFT joins return the same **26,428 rows with 0 nulls**, which confirms referential integrity before any analysis is built on the join. With `HAVING`, I found that the **New York Yankees** were the only franchise whose average player salary exceeded $7.5M in a season (2005, 2009, 2010, 2014, and 2016).

```sql
WITH payroll AS (
    SELECT teamID, yearID, SUM(salary) AS totalPayroll
    FROM Salaries GROUP BY teamID, yearID
),
homeruns AS (
    SELECT teamID, yearID, MAX(HR) AS maxHR
    FROM Teams GROUP BY teamID, yearID
)
SELECT p.teamID, p.yearID, p.totalPayroll, h.maxHR
FROM payroll p
JOIN homeruns h ON p.teamID = h.teamID AND p.yearID = h.yearID
WHERE p.totalPayroll > 150000000 AND h.maxHR >= 30
ORDER BY p.totalPayroll ASC
LIMIT 5;
```

### 3. Database automation with triggers and transactions (Projects 8–9)
I designed a new table, filled it with **5,149 records** using `INSERT ... SELECT` and a correlated subquery (each player's most recent team), and changed its schema. I then wrote triggers that **automatically keep a related table in sync** when new records arrive, and used savepoints to make multi-row inserts atomic and reversible.

```sql
CREATE TRIGGER IF NOT EXISTS update_deathYearMonthDay
AFTER INSERT ON DeathRecords
FOR EACH ROW
BEGIN
    UPDATE People
    SET deathYear = NEW.yearID, deathMonth = NEW.monthID, deathDay = NEW.dayID
    WHERE People.playerID = NEW.playerID;
END;
```

### 4. Turning NoSQL data into insights (Project 10)
I loaded 45,466 movies into MongoDB and used a `$switch` aggregation pipeline to group films into popularity tiers. The result: **average rating rises with each popularity tier**, from 6.01 for low-popularity films to 7.83 for high-popularity films.

### 5. Query optimization and joining MongoDB with pandas (Project 11)
I joined orders to products with `$lookup` to compute **revenue by category**. I created compound, multikey, text, and unique indexes and checked them with `explain()`. I also moved the data into pandas to analyze inventory value, customer preferences, and monthly order status (using a pivot table).

```python
revenue_pipeline = [
    {"$unwind": "$items"},
    {"$lookup": {"from": "products", "localField": "items.product_id",
                 "foreignField": "product_id", "as": "product_info"}},
    {"$unwind": "$product_info"},
    {"$group": {"_id": "$product_info.category",
                "revenue": {"$sum": {"$multiply": ["$items.price", "$items.quantity"]}}}},
    {"$sort": {"revenue": -1}}
]
# Electronics: $2,979.93 | Sports: $1,074.90 | Kitchen: $819.92
```

---

## What This Coursework Prepared Me For

| Role | Relevant experience from this repo |
|---|---|
| **Data Analyst** | Answering business questions with SQL aggregations, `HAVING` filters, and pandas group-bys; turning query output into written findings |
| **Data Engineer** | ETL into MongoDB, schema design and changes, triggers, transactions, indexing, and checking data integrity after joins |
| **Data Scientist / ML (entry-level)** | Cleaning and profiling raw data at scale, handling missing and badly encoded values, building analysis-ready DataFrames from nested JSON |
| **Software / Backend Engineer** | Database design, CRUD operations, query performance tuning, Linux and HPC workflows, Python scripting |

---

## Repository Structure

```
tdm201/
├── README.md
├── Niharika_Rai_project1.ipynb          # Bash: profiling large files
├── Niharika_Rai_project2.ipynb          # Bash: Linux filesystem & HPC storage
├── Niharika_Rai_project3.ipynb          # Bash: grep, regex, and Unix pipelines
├── Niharika_Rai_project4.ipynb          # awk: analytics & reporting
├── Niharika_Rai_project5.ipynb          # SQL: fundamentals
├── Niharika_Rai_project6.ipynb          # SQL: joins & CTEs
├── Niharika_Rai_project7.ipynb          # SQL: advanced aggregation & multi-table joins
├── Niharika_Rai_project8.ipynb          # SQL: DDL / DML & schema changes
├── Niharika_Rai_project9.ipynb          # SQL: triggers, views & transactions
├── Niharika_Rai_mongodb_project10.ipynb # MongoDB: ingestion, queries & aggregation
└── Niharika_Rai_mongodb_project11.ipynb # MongoDB: advanced queries, pandas & indexing
```

## Running the Notebooks

The notebooks were written for Purdue's **Anvil** cluster and read datasets from `/anvil/projects/tdm/data/`, which is only available to The Data Mine. All outputs are saved in the notebooks, so you can review them directly on GitHub without running anything.

To re-run them in another environment:

1. Install the dependencies:
   ```bash
   pip install jupyter pandas pymongo ipython-sql
   ```
2. Get public copies of the datasets: the [Lahman Baseball Database](https://sabr.org/lahman-database/), [MovieLens / TMDB metadata](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset), [Amazon Fine Food Reviews](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews), and the [SF Bay Area Bike Share](https://www.kaggle.com/datasets/benhamner/sf-bay-area-bike-share) data.
3. Update the file paths in the notebooks to point to your local copies.
4. For Projects 10–11, start a local MongoDB server on `mongodb://localhost:27017/`.

---

## About The Data Mine

[The Data Mine](https://datamine.purdue.edu/) is Purdue University's large-scale living-learning community for data science. Its **Corporate Partners Program** pairs student teams with industry sponsors on real data science projects. TDM 201 builds the technical foundation for that work: practical, production-relevant skills on real datasets and real HPC infrastructure.
