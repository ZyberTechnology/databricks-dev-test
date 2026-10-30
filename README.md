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

The layer folders contain brief starting notes. Add source-specific notebooks
and tests as the dataset and requirements are defined. Avoid committing real or
sensitive source data to `data/landing`.

## Suggested workflow

1. Place a small, non-sensitive sample dataset in the landing area.
2. Build Bronze ingestion to preserve the source data and record ingestion
	 metadata.
3. Build Silver transformations to clean and validate the data.
4. Build Gold tables around the reporting questions the project needs to answer.
5. Test transformations and data quality rules before running the pipeline on
	 larger datasets.