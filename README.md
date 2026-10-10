# Pretty Hurts: Internalized Stigma and Mental Health in South Asian Women

> Python analysis of how internalized beauty norms (colorism, body hair stigma, hair texture bias, and body type expectations) relate to self-esteem and anxiety among South Asian girls and women, using Pearson correlation and k-means clustering.

---

## Overview

Beauty standards in many South Asian communities are passed down through family, media, and tradition. They often favor lighter skin, smooth or straight hair, and slim bodies, while stigmatizing darker skin, body hair, textured hair, and larger bodies. This project asks whether frequent exposure to these norms is associated with lower self-esteem and higher anxiety.

The study combines surveys, qualitative narratives, and data science tools. This repository contains the quantitative analysis code and the research poster.

## Study Design

| | |
|---|---|
| **Population** | South Asian females, ages 13-25 |
| **Sample size** | n = 29 |
| **Self-esteem** | Rosenberg Self-Esteem Scale (RSES) |
| **Anxiety** | GAD-7 (Generalized Anxiety Disorder scale) |
| **Beauty norm exposure** | Likert-scale items on frequency of appearance-based comments, pressure to conform, and family/social media influence |

Each participant has three composite scores, stored as lists in the script:

| Variable | Description |
|---|---|
| `BeautyNorms_Score` | Average frequency of experiencing beauty norms |
| `SelfEsteem_Score` | Average self-esteem score |
| `Anxiety_Score` | Average anxiety score |

## Analysis

The script runs two analyses for each outcome (self-esteem and anxiety), with `BeautyNorms_Score` on the x-axis in every plot:

1. **Pearson correlation** between beauty norm exposure and the outcome, with a scatter plot and least-squares trend line.
2. **K-means clustering** (`k = 3`, `random_state = 42`, `n_init = 10`) to group participants with similar score combinations, with cluster centers marked as red X's.

### Key Findings

| Relationship | Pearson r | p-value | Interpretation |
|---|---|---|---|
| Beauty norms vs. self-esteem | **-0.47** | 0.010 | Moderate negative, statistically significant |
| Beauty norms vs. anxiety | **+0.22** | 0.255 | Weak positive, not statistically significant |

- Higher exposure to beauty norms is associated with **lower self-esteem**.
- Higher exposure is also associated with **higher anxiety**, but the relationship is weaker and does not reach conventional significance at n = 29.
- **Clustering** reveals three groups in each analysis:
  - *Self-esteem:* higher self-esteem / lower exposure, a mid-range group, and low self-esteem / high exposure (possibly the most affected).
  - *Anxiety:* lower anxiety / lower exposure, a mid-range group, and high anxiety / moderate-to-high exposure.

The clusters suggest the impact of beauty norms is not uniform across individuals.

### Implications

The results point toward a need for culturally sensitive interventions, including media literacy, open family-based dialogue, and community programs that deconstruct harmful beauty standards.

## Repository Contents

```
.
├── README.md
├── survey_on_cultural_beauty_norms_and_mental_wellbeing.py   # Analysis code
└── SAMHC_Final_Poster_by_Anya_Deshpande.pdf                  # Research poster
```

## Getting Started

### Requirements

- Python 3.8+
- `numpy`
- `matplotlib`
- `scipy`
- `scikit-learn`

```bash
pip install numpy matplotlib scipy scikit-learn
```

### Run

```bash
python survey_on_cultural_beauty_norms_and_mental_wellbeing.py
```

The script prints the correlation results to the console:

```
BeautyNorms vs SelfEsteem: r = -0.47, p = 0.010 (n = 29)
BeautyNorms vs Anxiety: r = 0.22, p = 0.255 (n = 29)
```

and opens four plots, one after another:

1. Self-esteem vs. beauty norms (scatter with trend line)
2. Anxiety vs. beauty norms (scatter with trend line)
3. K-means clustering of self-esteem vs. beauty norms
4. K-means clustering of anxiety vs. beauty norms

Close each plot window to see the next one. To run without a display (e.g., on a server), set `MPLBACKEND=Agg`.

### Code structure

| Function | Purpose |
|---|---|
| `correlation(x, y, x_name, y_name)` | Prints and returns Pearson r and p-value |
| `plot_scatter_with_trend(...)` | Scatter plot with a least-squares trend line |
| `cluster_and_plot(...)` | Runs k-means on two scores, plots clusters and centers, returns labels and centers |

To change the number of clusters, edit `N_CLUSTERS` at the top of the script.

## Limitations

This is a small, exploratory project, and results should be read accordingly.

- **Small sample (n = 29)** limits statistical power and generalizability.
- **Correlation is not causation.** The data cannot show that beauty norms *cause* lower self-esteem or higher anxiety.
- **Self-selected survey sample**, so participants may not represent all South Asian girls and women.
- **Clustering with k = 3** was chosen for demonstration rather than validated (e.g., via the elbow method or silhouette score), and k-means on 29 points is sensitive to initialization.
- The anxiety correlation is not statistically significant.

## Future Work

- Increase sample size and recruit more broadly across South Asian subgroups
- Validate the number of clusters (elbow method, silhouette analysis)
- Control for age, region, and generational factors
- Analyze the qualitative narratives alongside the quantitative scores
- Explore regression models and subscale-level analysis (colorism, hair, and body type separately)

## Disclaimer

This is a student research project and is not a clinical study or a diagnostic tool. If you or someone you know is struggling with self-esteem, body image, or anxiety, please reach out to a qualified mental health professional.
