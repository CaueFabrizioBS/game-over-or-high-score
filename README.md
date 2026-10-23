# Game Over or High Score? (Video Game Sales Analysis)

An analysis of historical video game sales for **Ice**, an online store that sells games worldwide. The goal is to find the patterns that make a game successful, so the store can spot potential best sellers and plan its advertising campaigns for 2017.

The data goes up to 2016 and includes sales by region, platform, genre, release year, critic and user scores and ESRB rating. The project follows the full workflow of a data analysis: data cleaning, exploratory analysis, regional profiles and hypothesis testing.

## Main findings

* **Platforms have a clear life cycle.** The most successful ones last 10 to 11 years, while a typical platform stays active for about 6 to 7. Sales usually peak 4 to 5 years after launch.
* **Only recent data matters for 2017.** The analysis focuses on 2013 to 2016, when PS4 and Xbox One opened the current generation.
* **PS4 is the clear leader,** followed by Xbox One. PS3 and X360 still show high totals, but their sales are falling fast, and Wii U is new but already declining.
* **A few hits carry the market.** On every platform, half of the games sell less than about 200 thousand copies, and the gap between platforms comes from their biggest hits.
* **Shooters are the safest genre per title.** A typical shooter sells about 450 thousand copies, against 110 thousand for action, which has the highest total but depends on a few blockbusters.
* **Critic scores matter a bit, user scores barely do.** The correlation between critic score and sales stays between 0.33 and 0.42 on every leading platform. User scores only show some relation to sales on Nintendo platforms.
* **Each region plays its own way:**
    * **North America:** Sony and Microsoft split the market almost evenly, and M rated games take about 37% of sales.
    * **Europe:** PlayStation dominates, with PS4 alone holding about a third of the market.
    * **Japan:** 3DS has almost half of the market, role-playing games lead, and shooters barely make the top 5.
* **Hypothesis tests:** there is no evidence that Xbox One and PC have different average user scores (p ≈ 0.15), but action and sports do (p ≈ 0, with averages of 6.84 and 5.24).

## What the notebook does

1. **Data overview:** loads the 16,715 rows and checks types, missing values and duplicates.
2. **Data cleaning:**
    * Standardizes column names and text values (lowercase, no extra spaces).
    * Merges two split records (Madden NFL 13 and Sonic the Hedgehog on PS3) by summing their sales.
    * Removes rows without name, genre or year (about 1.6% of the data), labels missing ESRB ratings as `'unknown'` and keeps missing scores as NaN, after checking the likely reasons for each gap.
    * Treats `'tbd'` in `user_score` as a missing value and fixes the data types.
    * Corrects a DS game listed as released in 1985, before the console existed.
    * Adds a `total_sales` column (16,443 rows remain).
3. **Exploratory analysis:** games per year, sales and life cycle of each platform, choice of the relevant period, box plots of sales per platform and per genre, and correlation between review scores and sales.
4. **Regional profiles:** top 5 platforms and genres in North America, Europe and Japan, and the effect of the ESRB rating on sales.
5. **Hypothesis testing:** two Welch's t-tests with `scipy.stats.ttest_ind` (α = 0.05).
6. **Conclusion:** a campaign plan for 2017 by region.

## Viewing the notebook

The charts were made with Plotly, which GitHub does not render. To see them, open the notebook on **[nbviewer](https://nbviewer.org/github/CaueFabrizioBS/game-over-or-high-score/blob/main/game_over_or_high_score_analysis.ipynb)** or run it locally.

## Repository structure

```
game-over-or-high-score/
├── datasets/
│   └── games.csv
├── game_over_or_high_score_analysis.ipynb
├── README.md
└── requirements.txt
```

## Run locally

```
git clone https://github.com/CaueFabrizioBS/game-over-or-high-score.git
cd game-over-or-high-score
python -m venv venv
venv\Scripts\activate          # Windows
source venv/bin/activate       # macOS / Linux
pip install -r requirements.txt
pip install ipykernel           # to run the notebook in VS Code or Jupyter
```

Then open `game_over_or_high_score_analysis.ipynb` and run all cells. The notebook reads the data from the `datasets/` folder, so it must be opened from the project root.

## Tech stack

Python, pandas, Plotly Express, statsmodels, SciPy, Jupyter Notebook.
