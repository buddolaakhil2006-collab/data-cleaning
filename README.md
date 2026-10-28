# Data Cleaning — CodeNova Data Science Task 2

A reproducible data-quality audit and cleaning pipeline for a deterministic fictional retail sales dataset. The original raw CSV is retained unchanged; the script writes standardized output under `data/sales_clean.csv`.

> **Synthetic data:** the assignment brief supplied no sales dataset. This project uses locally generated fictional records (seed 42), not real company or customer data.

## Deliverables

- `src/clean_data.py` — automated, reproducible cleaning and audit report generation.
- `src/generate_sales_data.py` — deterministic raw-data generator with intentional data-quality issues.
- `data/sales_raw.csv` — unchanged generated source, including missing values, duplicate records, invalid types, and invalid values.
- `data/sales_clean.csv` — standardized output.
- `reports/task2_data_quality_audit.md` — Markdown audit with cleaning rationale, before/after metrics, and limitations.
- `reports/before_after_profile.csv` — machine-readable quality and descriptive-statistics comparison.

## Cleaning summary

The pipeline removes exact duplicate rows, parses dates and numeric columns, drops missing/unparseable dates (they cannot be inferred without distorting time trends), converts impossible values to missing, imputes numeric fields with post-deduplication medians and categories with modes, and flags potential 1.5×IQR outliers without automatically clipping plausible large orders. The current generated run reduces **1,827 rows to 1,773**, with **0 missing cells and 0 exact duplicates** after cleaning. See the audit report for exact counts, values, cutoffs, and rationale.

## Run locally

From the repository root, with Python 3.10+:

```bash
python -m pip install -r requirements.txt
python src/generate_sales_data.py
python src/clean_data.py
```

The generator uses a fixed seed for reproducibility. The cleaner reads the raw CSV and writes only the clean CSV and report files.

## Limitations

This example demonstrates a workflow on synthetic data. Median/mode imputation can compress variation, and IQR outlier flags require contextual review before any removal. Production cleaning should be agreed with data owners and reconciled to source records.
