# NYC Airbnb Listings — Reproducible Data Workflow

**Author:** Md Hafizur Rahman Bhuia

A complete, reproducible data-science workflow built on the NYC Airbnb Listings dataset. It ingests the raw data, cleans and transforms it with documented, reusable functions, runs exploratory analysis, and produces labeled visualizations—all version-controlled with Git so the entire pipeline can be rerun from scratch.

> Note: This README contains only run-time instructions and brief reflection. For detailed methodology, interpretations, academic citations, and the full workflow description, see **`module_summary.md`**.

---

## What I Built

A modular, error-free Jupyter notebook (`data_workflow.ipynb`) that implements a professional data workflow:

- **Ingestion** — loads the dataset with Pandas and confirms it loaded correctly.
- **Cleaning** — two reusable, documented functions (`clean_structure`, `clean_missing`).
- **Exploratory analysis** — one EDA function (`explore_data`) printing null counts, grouped price statistics, property mix, and numeric summaries.
- **Visualizations** — three labeled plots (bar, violin, FacetGrid boxplots).
- **Summary** — interpretation of results, limitations, and assumptions.

---

## Dataset

- **Name:** NYC Airbnb Open Data
- **Link:** https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data
- **Local file:** `data/AB_NYC_2019.csv` (place the CSV here before running)
- **Scope of analysis:** nightly `price` by `neighbourhood_group` and `room_type` (~48,000 listings)

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/hafizur-rahman/ai-programming-foundations-project.git
cd ai-programming-foundations-project
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv .venv
# On macOS/Linux:
source venv/bin/activate
# On Windows:
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

> `requirements.txt` was generated with `pip freeze > requirements.txt` so the environment can be reproduced exactly.

### 4. Add the dataset

Place the CSV at `data/AB_NYC_2019.csv`. The notebook will raise a clear error if the file is missing.

### 5. Open and run the notebook

```bash
jupyter lab            # or: jupyter notebook
```

Then open `data_workflow.ipynb` and **Run → Run All Cells** to execute the workflow end-to-end. All charts are saved automatically to `charts/`.

---

## Project Structure

```
.
├── data/
│   └── AB_NYC_2019.csv      # dataset (place here)
├── charts/                   # saved figures (auto-generated)
├── data_workflow.ipynb       # main notebook (the workflow)
├── module_summary.md         # detailed report + citations
├── requirements.txt          # pinned dependencies
└── README.md
```

---

## Version Control

- Multiple commits track progress through each task.
- A dedicated development branch is used for experimental work, keeping `main` as the stable release branch.

---

## Bias Awareness

Poor data handling can distort real-world conclusions:

- **Dropping rows with missing neighbourhood labels** may remove a non-random subset (e.g., less-popular listings), biasing borough statistics.
- **Median imputation** assumes missing values are missing at random and erodes the uncertainty of imputed prices.
- **Removing shared-room listings** changes the population of interest, so results describe whole-property rentals, not the entire market.

Mitigation: every cleaning step is documented as an explicit assumption, dataset sizes are reported before and after cleaning, and boroughs with few listings are flagged as statistically unstable.

---

## Future Integration

- **Machine learning:** The cleaned frame can feed a supervised regression model (e.g., predicting `price`). Categorical variables (`neighbourhood_group`, `room_type`) would need encoding, and `reviews_per_month` / availability features would expand the predictor set.
- **Neural network preparation:** Numeric features would be standardized, the target log-transformed to match its skewed distribution, and the data split into train/validation/test sets.
- **Agentic automation:** The modular function design (`clean_structure`, `clean_missing`, `explore_data`) maps naturally to an agent pipeline—an agent could invoke each stage, validate outputs, and iterate on cleaning heuristics autonomously.

See `module_summary.md` for the full rationale and scholarly citations.

---