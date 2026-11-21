# AI, Social Media and Student Health: EDA and Dimensionality Reduction

Exploratory data analysis (EDA) of a dataset on how social media and AI tool usage relate to sleep, physical activity,
and the mental and physical health of students. The data is described with statistics and plots and then visualised
in a reduced space with four methods:

- **PCA on the covariance matrix**
- **PCA on the correlation matrix**
- **MDS**, metric and non-metric, with a Stress vs. number of dimensions plot
- **t-SNE**

Finally, the analysis checks whether outliers can be located on the maps and whether every method points to the same observations.

> The notebook itself (descriptions, tables and plot labels) is written in Polish.

## Data

[AI & Social Media Impact: Student Health & Grades](https://www.kaggle.com/datasets/srisyra02/ai-and-social-media-impact-student-health-and-grades) (Kaggle, CC0 license).
16,000 observations and 10 variables: age, gender, education level, daily social media hours, daily AI tool hours,
sleep hours, physical activity hours, mental health score and physical health score (0–100).

The data is not stored in the repository. The notebook downloads it from Kaggle on every run (the page URL is in the `database` file).

## What the analysis covers

| Step | Contents |
|---|---|
| Data overview | origin, variable table (type, missing values), descriptive statistics, category counts and percentages |
| Distributions | histograms (√n bins) and box plots for all quantitative variables |
| Matrices | heatmaps of the covariance and correlation matrices |
| PCA | eigenvalues, number of components for 90/95/99% of variance, 2D and 3D maps, equations of the first three components |
| MDS | 2D and 3D maps (metric and non-metric), Stress-1 for 1–6 dimensions |
| t-SNE | 2D and 3D maps of all 16,000 observations |
| Outliers | Hotelling's T² in PCA, compared with MDS, t-SNE (LOF) and Mahalanobis distance |

## Key findings

- The data is most likely **synthetic**: no missing values, truncated distributions with a spike at 0 h, and a uniformly
  distributed age that is unrelated to any other variable.
- **Covariance PCA** is dominated by the scale of the health scores (0–100): two components carry 88.4% of the variance.
  After standardisation (**correlation PCA**) two components carry only 46.3%, because the variables are weakly correlated (|r| ≤ 0.42).
- In correlation PCA, PC1 is a "healthy lifestyle" axis (sleep, activity, health) opposed to time spent on social media.
- **MDS** reproduces the PCA layout, with a 2D Stress-1 of 0.24–0.28 (poor fit). **t-SNE** shows no clusters.
- The six PCA outliers match those found with MDS, but not with t-SNE, which preserves local neighbourhoods rather than distance from the centre.

## Running

```bash
python -m venv .venv
.venv\Scripts\activate          # Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
```

Open `analyzis.ipynb` in VS Code (Jupyter extension) or Jupyter Lab and select the `.venv` kernel. Plots are interactive (plotly).

## Type checking

```bash
pip install -r requirements-dev.txt
nbqa mypy analyzis.ipynb
```

mypy checks the notebook's code cells through `nbqa`. The mypy configuration is in `pyproject.toml`.

## Tech stack

Python, pandas, NumPy, SciPy, scikit-learn (PCA, MDS, t-SNE, LOF), plotly, mypy.

## Authors

- Marek Turkowicz ([@MarekTurkowicz](https://github.com/MarekTurkowicz))
- Emilia Nodzewska ([@emilia-nodz](https://github.com/emilia-nodz))
