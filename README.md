# Portfolio analysis as a service: Horizon Europe projects on a policy topic

Annex to a written note on how a Feedback to Policy team can turn a broad question from a policy unit ('What has Horizon Europe funded in our area, and what should we take into the next calls?') into a documented, reusable data service. The notebook shows the first analytical step, using public data only.

## What the notebook does

1. Downloads the public CORDIS file of Horizon Europe projects and records the download date and a fingerprint of the file, so that results can be reproduced.
2. Checks data quality: duplicates, missing fields, plausible dates and amounts. It repairs rows where the separator character appears inside the free-text columns (project description or keywords), checks that every repaired row has its fields in the right place, converts amounts written with a decimal comma, and compares the total EU contribution with the Commission's published figure.
3. Reads the policy unit's topic definition: a small table of terms marked *core* or *related*. **The terms are illustrative** ('nature-based solutions'); in a real request the policy unit provides and confirms them.
4. Selects the matching projects and records, for each one, which terms matched and in which fields.
5. Summarises the portfolio: number of projects, maximum EU contribution, start year, type of action, coordinator country and project status. It also compares the selection with CORDIS's EU biodiversity spending tracker, to show whether an existing classification could replace the agreed definition.
6. Exports the selection for review by the policy unit, with a link to each project's CORDIS page and empty *include (yes/no)* and *comment* columns.

## Reading the results without running anything

Open [`portfolio_analysis.ipynb`](portfolio_analysis.ipynb) on this page: the explanations, tables and chart display in the browser. The review file is [`outputs/projects_for_review.csv`](outputs/projects_for_review.csv).

## Running it yourself

Requirements: Python 3.13 and an internet connection for the first run (the CORDIS file is about 37 MB).

```
python -m venv .venv
.venv\Scripts\activate            # on macOS or Linux: source .venv/bin/activate
pip install -r requirements.txt
```

Then open `portfolio_analysis.ipynb` in VS Code or Jupyter and run all cells. After the download, the notebook runs in under a minute.

## Repository structure

```
f2p-portfolio-analysis/
├── README.md                                   this file
├── portfolio_analysis.ipynb                    the analysis, with explanations and results
├── requirements.txt                            Python packages and versions used
├── LICENSE                                     EUPL-1.2
├── inputs/
│   └── topic_definition_illustrative.csv       the policy unit's topic definition (illustrative)
├── outputs/
│   └── projects_for_review.csv                 selection for review, created by the notebook
└── data/raw/                                   CORDIS download, created by the notebook (not stored here)
```

## Data source and reuse

- **Source:** CORDIS, [EU research projects under Horizon Europe (2021-2027)](https://data.europa.eu/data/datasets/cordis-eu-research-projects-under-horizon-europe-2021-2027), European Commission, published on data.europa.eu.
- **Reuse:** under the European Commission reuse notice. The data are downloaded by the notebook and are not redistributed in this repository.
- **Field definitions:** in the documentation file included in the CORDIS download (`documentation.zip`).
- **Personal data:** none used. The analysis uses project-level fields and the country and role of participating organisations.

## Assumptions and limitations

- The topic definition is illustrative and would be agreed with the policy unit.
- Matching on terms misses projects that use other words and includes some that use a term in another sense; the review step measures both.
- The file describes what was funded, not what came out of it. Results are published in separate CORDIS files, and most projects are still running.
- Figures reflect the file downloaded on the date recorded in the notebook.
- EU contribution is the maximum amount committed in the grant agreement, not the amount paid.

## How this was prepared

A generative-AI assistant was used to search public sources, draft text and write the notebook code. The author took the decisions on scope, data and method, reviewed each part, ran and published the notebook, and is responsible for the content.

## Licence

The code and text in this repository are licensed under the [European Union Public Licence v. 1.2](LICENSE) (EUPL-1.2).
