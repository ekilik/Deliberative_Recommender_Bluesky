# Democratic News Recommendations for Ideological Diversity on Platforms: A User Experiment on Bluesky

Analysis code for the paper. With the anonymized data, which are available upon request, the
notebooks reproduce every table, figure and statistic reported in it. The code of the Bluesky ranker pipeline will be released separately upon
publication.

## Abstract

Social media platforms have become one of the main sources of news, and their engagement-driven
algorithmic curation increasingly shapes which news users encounter. Diversity-aware news
recommenders have been proposed as a way to realize exposure diversity, but they have mostly been
evaluated offline or in dedicated news apps rather than in live social media feeds. We develop and
deploy a diversity-aware ranker for news posts on Bluesky, using the platform’s open protocol to
serve custom feeds within participants’ regular platform use. Our ranker pipeline clusters articles
from eight popular Flemish news outlets into events, links named entities to politicians and their
parties, and classifies these as left, center or right using the 2024 Chapel Hill Expert Survey.
Informed by the deliberative model of democracy, the ranker then selects the articles that maximize
the entropy of left, center and right party visibility across the feed. In a user experiment, we
randomly assigned participants to this diversity-aware feed or to a control feed that selected the
most recent article from each event cluster. Participants’ activity, engagement and satisfaction
did not differ between conditions, suggesting that diversification may not necessarily involve a
trade-off. Perceived diversity also did not differ between conditions although the treatment feed
was significantly more diverse on all 27 days across 1,295 ranking cycles. Nearly half of political
event clusters mentioned parties from only one ideological category, which exemplifies the
dependence of algorithmic diversification on the diversity of the news supply.

## Repository structure

```
├── data/               codebook of the analysis data (data available upon request)
├── scripts/            one notebook per part of the paper, numbered in the paper's order
├── tables_figures/     tables and figures written by the notebooks
└── requirements.txt
```

| Notebook | Paper section | Produces |
|---|---|---|
| `01_descriptives.ipynb` | Measures | Table 1, Tables B1 and B2, Cronbach's α of the diversity-seeking scales |
| `02_balance_checks.ipynb` | Participants | Tests of differences between conditions in demographics and control variables |
| `03_treatment_check.ipynb` | Methodology; Treatment Check | Figures 1 to 3 and the treatment-check statistics |
| `04_RQ1_engagement.ipynb` | User Activity and Engagement (RQ1) | Figures 4 and 5, Welch's *t*-tests |
| `05_RQ2_user_satisfaction.ipynb` | User Satisfaction (RQ2) | Figures 6 to 8, Welch's *t*-tests |
| `06_RQ3_perceived_diversity.ipynb` | Perception of Diversity (RQ3) | Figures 9 and 10, Welch's *t*-tests |
| `07_correlations_all_variables.ipynb` | Exploratory Analyses | Figure 11, Spearman correlations with Benjamini–Hochberg correction |

Each notebook reads only from `data/` and runs independently of the others.

## Data

The data are not included in this repository and are available from the authors upon request.
They consist of the two analysis samples (participants who completed the onboarding survey and
were active on the feed, N = 74; those who also completed the offboarding survey, N = 56) and
feed-level data of the treatment check. Participants are identified only by the Bluesky study
accounts the research team created for the experiment. [`data/README.md`](data/README.md)
describes the files and variables. Place the files in `data/` to run the notebooks.

## Reproducing the analyses

With Python 3.10:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Then open the notebooks in `scripts/` (`jupyter lab`) and run them, or run all of them from the
command line:

```bash
jupyter nbconvert --to notebook --execute --inplace scripts/*.ipynb
```

Tables (`.docx`) and figures are written to `tables_figures/`.

## How to cite

<!-- Add the reference and DOI once the paper is published. -->

## License

The code is released under the MIT License. See [`LICENSE`](LICENSE).
