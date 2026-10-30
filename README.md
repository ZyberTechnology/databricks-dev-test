# databricks-dev-test

This is my first project, and I am developing it step by step. The project is
currently in progress. I will update this README as I add features and document
how to set up and use the project.

## Project structure

This project uses the Medallion architecture to organize data as it moves
through the pipeline:

```text
data/
	landing/             Source files waiting to be ingested
notebooks/
	bronze/              Ingest source data with minimal changes
	silver/              Clean, validate, and standardize data
	gold/                Prepare trusted data for reporting and analysis
tests/                 Tests for transformations and data quality rules
```

The layer folders contain a notebook for each stage: `bronze/bronze_ingest.ipynb`,
`silver/silver_clean.ipynb`, and `gold/gold_powerbi_publish.ipynb`. Run them in
that order. The starter notebooks read CSV files from the Unity Catalog volume
`/Volumes/superpower/bronze/landing` and write tables under the `superpower`
catalog. Each run replaces its output table with the current result. Avoid
committing real or sensitive source data to `data/landing`.

The Gold notebook publishes `superpower.gold.pbi_dataset` and
`superpower.gold.ingestion_summary`. These are starter reporting tables; add
source-specific types, business measures, and dimensions before building
production Power BI reports.

## Suggested workflow

1. Place a small, non-sensitive sample dataset in the landing area.
2. Build Bronze ingestion to preserve the source data and record ingestion
	 metadata.
3. Build Silver transformations to clean and validate the data.
4. Build Gold tables around the reporting questions the project needs to answer.
5. Test transformations and data quality rules before running the pipeline on
	 larger datasets.