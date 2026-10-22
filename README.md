# Streaming Homepage Optimization via Sequential Experimentation

Sequential factorial experiments on a simulated streaming platform ("Webflix") to find the homepage UI settings that minimize user browse time.

**Result:** A 25% tile size with a 0.5-second preview delay reduced average browse time by **15%**, from 16.7 min under the default settings to **14.2 min** (95% CI: 14.09–14.31).

## Problem

Streaming users facing too many choices can experience decision paralysis. They browse longer and sometimes leave without watching anything. This project uses controlled experiments to identify which homepage design factors affect browse time, and to find the configuration that minimizes it.

Data comes from a course-provided web simulator. We submitted experimental designs and received simulated per-user browse times. Each experiment drew on a limited budget of experimental units.

## Factors

| Factor | Description | Range | Default |
|---|---|---|---|
| Tile Size | Tile height as % of screen height | 10–50 | 20 |
| Preview Delay | Seconds between hover and preview autoplay | 0–2 | 1 |
| Preview Type | Teaser/trailer (TT) or actual content (AC) | {TT, AC} | TT |
| Play Something | Button that plays a personalized random title | {N, Y} | N |

## Approach

| # | Design | Goal | Finding |
|---|---|---|---|
| 1 | 2⁴ full factorial (16 conditions) | Screen all 4 factors and their interactions | Only Tile Size, Preview Delay, and their interaction were significant |
| 2 | 5×5 factorial (Tile Size × Preview Delay) | Locate the optimal region | Optimum near Tile Size 20–30, Preview Delay 0.5 |
| 3 | 3×2 factorial (Tile Size × Play Something) | Recheck a borderline interaction from Exp. 1 (p = 0.07) | Not significant (p = 0.58); Play Something dropped |
| 4 | 5×3 grid search (Tile Size × Preview Delay) | Pinpoint the optimum | Tile Size 25, Preview Delay 0.5 beat all 14 other conditions |

## Methods

- **Design:** full factorial designs, then a finer grid search around the optimal region
- **Sample size:** power analysis (α = 0.01, power = 0.99), with variance estimates updated after each experiment
- **Modeling:** OLS regression with effect-coded factors; partial F-tests to compare nested models
- **Comparisons:** F-tests for equal variances, Student's and Welch's t-tests
- **Multiple testing:** Bonferroni and Holm corrections

## Repository Structure

```
├── final_project.ipynb   # Analysis notebook
├── data/                 # Simulator output CSVs for each experiment
├── report.pdf            # Final written report
└── README.md
```

## Running the Notebook

```bash
pip install pandas numpy statsmodels scipy matplotlib seaborn
jupyter notebook final_project.ipynb
```

## Team

Amy Nguyen, Borna Karimi, Vu Chu-Le. Built for MSDS 629: Experiments in Data Science at the University of San Francisco (Jan 2026).
