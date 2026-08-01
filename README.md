# InternSpark Task 3 — README

**Project:** Alfido Tech Data Science Internship — Beginner Task
**Notebook:** `Instagram_Data_Analysis.ipynb`
**Dataset source:** [Kaggle — bhanupratapbiswas/instgram](https://www.kaggle.com/datasets/bhanupratapbiswas/instgram)

## Dataset description

The dataset is **relational**, not a single flat "posts" table. It ships as 7 CSVs modeling a simplified Instagram-style schema:

| File | Rows | Description |
|---|---|---|
| `users.csv` | 100 | Accounts: name, signup date, public/private, post count, verified status |
| `photos.csv` | 257 | Posts: image link, owning user, created date, filter used, content type (photo/video/carousel) |
| `likes.csv` | 8,782 | One row per like: liking user, photo, timestamp, like type |
| `comments.csv` | 7,488 | One row per comment: text, user, photo, timestamp, emoji used, hashtag count |
| `follows.csv` | 7,623 | Follower → followee edges, account status |
| `tags.csv` | 21 | Tag vocabulary (text + location) |
| `photo_tags.csv` | 501 | Tags applied to specific photos |

To analyze it we joined/aggregated these tables into two working views: a **post-level engagement table** (likes, comments, engagement rate) and a **user-level table** (follower/following counts, signup date).

## How to run

1. Place all 7 CSVs in a `data/` folder next to the notebook (already included in this delivery).
2. Open `Instagram_Data_Analysis.ipynb` in Jupyter or upload it to Google Colab (upload the `data/` folder too, or mount Drive).
3. Run all cells top to bottom — the notebook is fully self-contained (loads data → cleans → engineers features → visualizes → tests → recommends).

## Initial observations (data quality)

These are the findings that shaped the rest of the analysis — worth reading before the notebook's charts:

1. **No missing values anywhere.** All 7 tables are fully populated.
2. **Timestamps are placeholders, not real activity times.** Every row in `photos`, `likes`, `comments`, `follows`, and `tags` shares the *exact same* `created time` value (`13-04-2023 08:04`) — the moment the file was exported, not when a post/like/comment actually happened. Only `users.created time` (account signup) has genuine date variation (2016–2017). **This means a real "best time to post" analysis cannot be derived from this file** — we say so explicitly in the notebook rather than manufacturing a pattern from a constant.
3. **The follower graph is near-uniform.** Every account has roughly the same follower count (~76, std ≈ 0.4) and follows almost all other accounts — a pattern consistent with randomly generated test data rather than an organic social network.
4. **No statistically significant engagement drivers.** We tested content type, filter use, hashtag count, and verified status against engagement rate (ANOVA / t-tests / correlation) — none were significant at p < 0.05.

**Conclusion:** this dataset is a well-known public schema commonly used for SQL/relational-database practice. It's a good sandbox for practicing the full EDA → feature engineering → visualization → hypothesis-testing pipeline (which the notebook does end-to-end), but its posting-time and engagement-driver signals should **not** be treated as evidence about real Instagram behavior. The notebook's Recommendations section is built accordingly: what's genuinely supported by the data is kept separate from general industry best-practice guidance, and both are labeled as such.

## Deliverables in this package

- `Instagram_Data_Analysis.ipynb` — full notebook (EDA, feature engineering, 8 visualizations, statistical tests, findings, recommendations)
- `data/` — the 7 source CSVs
- `README.md` — this file
- `Alfido_Tech_Instagram_Strategy.docx` — one-page strategy document (content calendar + 5 engagement strategies), delivered separately
