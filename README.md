# Netflix Dataset — Visualization & Insights (Power BI)

An exploratory data analysis and dashboarding project on Netflix's movies and TV shows catalog, built in Power BI. The goal is to clean a real-world dataset, model it meaningfully, and answer a set of business-style questions through visuals.

## Dataset

- **Source:** Netflix TV Shows and Movies dataset
- **Size:** ~5,283 records
- **Coverage:** Titles released between 1953–2022 (with some gaps in early years, e.g., 1955, 1957)
- **Type:** Mix of Movies and TV Shows

### Key Fields

| Field | Description |
|---|---|
| `id` | Unique identifier per title; useful for counts and trend calculations |
| `title` | Name of the movie/show |
| `type` | MOVIE or SHOW |
| `release_year` | Year of release |
| `description` | Short synopsis (not used directly in this analysis, but a candidate for future NLP/genre extraction) |
| `age_certification` | Age rating; missing for a large portion of records and left as-is |
| `runtime` | Duration in minutes |
| `imdb_score` | IMDb rating |
| `imdb_votes` | Number of IMDb votes; some records have this missing |

## Questions Answered

1. Which was the best movie and TV show overall in the last 50 years?
2. How many titles do we have across the last few years — is the dataset skewed toward recent releases?
3. On average, how has the IMDb score trended over the last 50 years?
4. Have more people started voting on IMDb over the last 50 years?
5. On average, how has runtime changed over the last 50 years?
6. How does age certification affect a title's rating?

## Approach

### 1. Data Cleaning (Power Query)
- Dropped non-analytical columns (`index`, `imdb_id`)
- Handled missing `imdb_votes` by excluding those rows from vote-based analysis rather than deleting them outright (they still hold value for other fields)
- Left missing `age_certification` values as-is — no reliable way to impute them

### 2. Feature Engineering
- Created a combined **`Rating*Votes`** column (`imdb_score × imdb_votes`) so that "best" titles reflect both quality *and* popularity — a single 9.5 rating from one voter shouldn't outrank a 9.0 rating from 50,000 voters
- Alternative approach considered: filtering to titles with `imdb_votes > 1000` to ensure statistical reliability

### 3. Visualizations
- **Slicers:** `release_year` (range) and `type` (Movie/Show)
- **Best title overall:** Column chart of title vs. `Rating*Votes`
- **Volume over time:** Line chart of distinct `id` count by `release_year`
- **Score trend:** Bar chart of average `imdb_score` by `release_year`
- **Voting trend:** Line chart of total `imdb_votes` by `release_year`
- **Runtime trend:** Line chart of average `runtime` by `release_year`
- **Age certification vs. rating:** Scatter plot of `age_certification` vs. average `imdb_score`

## Key Insights

- The dataset is heavily skewed toward titles released after 2010 — conclusions about long-term trends should account for this imbalance.
- The apparent rise in total IMDb votes over time is largely a byproduct of more recent titles existing in the dataset, not necessarily increased voter engagement per title — this trend was excluded from the final story for that reason.
- Average runtime has broadly decreased over the decades, though early-year trends (1950s–1990s) are based on very few data points and should be read cautiously.
- On average, TV shows rate higher than movies; within shows, **TV-14** rates highest, and within movies, **PG-13** rates highest.

## Tools Used

- **Power BI** — data modeling, DAX, visualization, and publishing
- **Power Query Editor** — cleaning and transformation


