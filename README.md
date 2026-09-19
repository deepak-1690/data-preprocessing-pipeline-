# Data Acquisition & Preprocessing Pipeline

A production-style Python pipeline for acquiring, validating, cleaning, and transforming raw data into clean, analysis-ready datasets — built as part of a data analytics coursework project (Week 2).

This repository accompanies the full strategy report:
docs/Data_Acquisition_and_Preprocessing_Strategy.docx

---

## Overview

| | |
|---|---|
| Objective | Build a robust, documented, and tested pipeline for sourcing, validating, cleaning, and transforming data prior to analysis |
| Language | Python 3.10+ |
| Core libraries | Pandas, NumPy, SciPy, Scikit-learn, Pandera, PyOD, Requests, BeautifulSoup, Matplotlib, Seaborn |
| Testing | Pytest, with unit tests for every pipeline stage |
| CI/CD | GitHub Actions — lint, format-check, and test on every push/PR |
| Deliverable | Strategy documentation (.docx) + a runnable, tested reference pipeline |

---

## Repository Structure

repo/
├── README.md
├── LICENSE
├── requirements.txt              # Pinned Python dependencies
├── pyproject.toml                # black / isort configuration
├── setup.cfg                     # flake8 / pytest configuration
├── .gitignore
├── .env.example                  # Template for environment variables
├── .github/
│   └── workflows/
│       └── ci.yml                # Lint, format-check, and test on push/PR
├── docs/
│   └── Data_Acquisition_and_Preprocessing_Strategy.docx
├── config/
│   └── source.yaml               # Data source configuration
├── data/
│   ├── raw/                      # Immutable, timestamped raw pulls (git-ignored)
│   └── processed/                # Cleaned, analysis-ready datasets (git-ignored)
├── src/
│   ├── extract.py                # Data extraction (APIs, downloads, scraping)
│   ├── validate.py               # Schema & integrity validation
│   ├── clean.py                  # Missing values, outliers, cleaning
│   ├── transform.py              # Scaling, encoding, feature engineering
│   └── pipeline.py               # Orchestrates the full run
├── notebooks/
│   └── eda_and_validation.ipynb  # Exploratory analysis & visual validation
└── tests/
    └── test_pipeline.py          # Unit tests for each pipeline stage

---

## Pipeline Workflow

Data Sourcing → Extraction → Raw Storage → Validation
   → Missing-Value Handling → Outlier Detection → Cleaning
   → Transformation → Processed Storage → Analysis-Ready Dataset

Each arrow above corresponds to a discrete, independently testable function. The full workflow diagram and pseudocode are in Section 8 of the strategy document.

---

## Getting Started

### Prerequisites
- Python 3.10 or higher
- pip / venv

### Installation

# 1. Clone the repository
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

# 2. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment variables (optional — only needed for authenticated sources)
cp .env.example .env
# then edit .env with your values

# 5. Run the pipeline
python src/pipeline.py --source-config config/source.yaml

### Configuration

Data sources are defined in config/source.yaml. Point it at any public CSV/JSON dataset URL, or change "type" to "api" / "web_table" as described in Section 3 of the strategy document:

type: file
location: "https://example.com/your-dataset.csv"
expected_columns:
  - column_1
  - column_2

---

## Running Tests

pytest tests/ -v

Tests cover schema validation, missing-value handling, outlier detection (IQR & Z-score), cleaning, and feature transformation — each function is tested in isolation using synthetic fixtures.

---

## Code Quality

This project enforces consistent style and catches issues automatically:

# Format code
black src tests

# Sort imports
isort src tests

# Lint
flake8 src tests

These checks run automatically via GitHub Actions on every push and pull request, across Python 3.10 and 3.11.

---

## Data Quality Approach

| Stage | Technique | Library |
|---|---|---|
| Validation | Schema & dtype checks, duplicate detection | Pandas, Pandera |
| Missing values | Mean/median/KNN imputation, missing-indicator flags | Scikit-learn |
| Outliers | IQR, Z-score, Isolation Forest | SciPy, Scikit-learn, PyOD |
| Cleaning | Type coercion, text normalization, de-duplication | Pandas |
| Transformation | Scaling, encoding, feature engineering | Scikit-learn, NumPy |

Full rationale for every technique and library choice — including trade-offs considered — is documented in the strategy report (Sections 4–7).

---

## Timeline

A 14-day execution plan (source setup → extraction → validation → cleaning → transformation → handoff) is detailed in Section 9 of the strategy document.

---

## Contributing

This is a coursework project, but suggestions and improvements are welcome:

1. Fork the repository
2. Create a feature branch (git checkout -b feature/your-feature)
3. Commit your changes with clear messages
4. Ensure black, flake8, and pytest all pass
5. Open a pull request

---

## License

This project is licensed under the MIT License — see LICENSE for details.
