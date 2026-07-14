# Netflix Shows & Movies — SQL Analysis

Exploratory analysis of Netflix's catalogue — roughly **5,850 titles** and **77k+ cast & crew credits** — using MySQL to break down what the library is actually made of: its ratings, genre mix, age certifications, production geography, and how it has grown over time.

**Tools:** MySQL
**Data:** [Netflix TV Shows and Movies — Kaggle](https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies)

## The dataset

Two related tables that link on `id`:

| Table | One row represents | Rows | Key fields |
|---|---|---|---|
| `titles` | a single movie or show | 5,850 | `title`, `type`, `release_year`, `age_certification`, `genres`, `production_countries`, `seasons`, `imdb_score`, `tmdb_score` |
| `credits` | one person credited on a title | 77,801 | `id` (→ `titles.id`), `name`, `character`, `role` |

The `id` key connects every actor and director to the titles they worked on — the basis for all cast and crew analysis.

## Why this project

Netflix's catalogue is large enough that patterns are invisible to the eye. The aim was to turn ~82k rows spread across two tables into clear answers about **content quality, content mix, and how the library has evolved** — the kind of view that supports content and acquisition decisions.

## Approach

1. Loaded both tables into a MySQL schema and related them on `id`.
2. Answered a set of business questions using `GROUP BY` / `HAVING` aggregation, `ORDER BY … LIMIT` rankings, `UNION ALL` comparisons, and joins across the two tables.
3. Summarized the findings per question (below).

## Questions explored & what I found

**1. The highest- and lowest-rated titles (by IMDB).**
The best-rated shows (Breaking Bad, Khawatir) sit around 9.5 and the strongest films around 9, while the bottom of the table falls to the low 2s. Ratings are a quick proxy for audience reception, and the spread shows how uneven that reception is across the catalogue.

**2. How the library splits across decades.**
Pre-2000 content is a tiny share of the library; the catalogue then explodes — **3,304 titles from the 2010s** and **1,972 already from the 2020s**. Netflix's library is overwhelmingly a library of recent content.

**3. Which age certifications dominate, and how they score.**
`R` is the single most common certification (**556** titles), followed by `PG-13` (451), `PG` (233), `G` (124) and `NC-17` (16). On average IMDB score, `TV-14` content rates highest — mature-leaning content both dominates the catalogue and tends to score well.

**4. The most common genres.**
Comedy is the most frequent genre for movies (384) and overall (484), with documentation and drama close behind; reality leads on the show side. Multi-genre combinations appear constantly, pointing to a catalogue that blends categories rather than sticking to single labels.

**5. Cast and crew.**
Joining `credits` to `titles` surfaces the most prolific actors and directors, the actors who appear most often in highly-rated titles (IMDB and TMDB above 8), and performers who played the same character across multiple titles.

## Key takeaways

- The catalogue skews heavily toward **recent** content (post-2010).
- **US production** dominates, with a long tail of other countries.
- **Mature certifications** (R, PG-13) are the most common.
- **Shows out-rate movies** on average, on both IMDB and TMDB.

## Repository

- `Netflix_SQL_Analysis.sql` — every query used in the analysis
- `titles.csv`, `credits.csv` — source data (from the Kaggle link above)

## To reproduce

1. Download the dataset from Kaggle.
2. Load both CSVs into a MySQL schema (the queries assume a schema named `shows_movies`).
3. Run `Netflix_SQL_Analysis.sql`.
