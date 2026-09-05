# **NYC Airbnb Listings — Reproducible Data Workflow**

**Author:** Md Hafizur Rahman Bhuia  
**Program:** Master's Degree in Artificial Intelligence — Capstone  
**Dataset:** NYC Airbnb Listings  
**Source:** [https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data)  

---

## **Project Description**

This project implements a complete, reproducible data‑science workflow using the NYC Airbnb Listings dataset. The workflow loads the raw dataset, applies structured cleaning functions, performs exploratory data analysis, generates labeled visualizations, and summarizes key findings. The design emphasizes modularity, transparency, and reproducibility—providing a strong foundation for later machine learning, deep learning, generative AI, and agentic AI projects in the capstone.

---

## **Reproducibility Instructions**

This project is designed to be fully reproducible. Follow the steps below to run the workflow:

### **1. Clone the Repository**
```bash
git clone https://github.com/hafizur-rahman/ai-programming-foundations-project.git
cd ai-programming-foundations-project
```

### **2. Create and Activate a Virtual Environment**
```bash
python -m venv .venv
source venv/bin/activate   # macOS/Linux
.venv\Scripts\activate      # Windows
```

### **3. Install Dependencies**
All dependencies are pinned in `requirements.txt`:
```bash
pip install -r requirements.txt
```

### **4. Run the Notebook**
Open and execute the notebook top‑to‑bottom:
```bash
jupyter notebook data_workflow.ipynb
```

The notebook will:
- Load the dataset
- Apply cleaning functions
- Run exploratory analysis
- Generate visualizations
- Produce summary outputs

## Dataset

- **Name:** NYC Airbnb Open Data
- **Link:** https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data
- **Local file:** `./data/AB_NYC_2019.csv` (committed to git for convenience)

---

## **Reflection Questions**

### **1. How does this workflow prepare me for machine learning?**

Machine learning depends on clean, well‑structured, well‑understood data. This workflow demonstrates the full preprocessing pipeline: ingestion, cleaning, outlier handling, feature understanding, and exploratory analysis. These steps mirror the exact preparation required before training supervised or unsupervised ML models. By building modular cleaning functions and structured EDA, the workflow ensures that future ML experiments can be run consistently and repeatably.

---

### **2. How does this workflow prepare me for deep learning?**

Deep learning requires strict reproducibility, stable preprocessing, and consistent data transformations. The use of:
- modular functions
- pinned dependencies
- documented transformations
- reproducible environment setup

directly supports deep learning workflows where data pipelines must be deterministic. This project establishes the habits needed for DL experiments: clean inputs, transparent transformations, and reproducible execution.

---

### **3. How does this workflow prepare me for agentic AI systems?**

Agentic AI systems rely on predictable data inputs, tool‑based workflows, and transparent state transitions. The modular cleaning functions, structured workflow, and reproducibility practices mirror the design patterns used in agentic systems:
- deterministic tools  
- clear preconditions  
- predictable outputs
- traceable transformations

This project builds the foundation for agents that can autonomously run data workflows, trigger analyses, or generate reports.

---

### **4. Where could poor data cleaning introduce bias?**

Bias can be introduced at multiple points in the cleaning process:

- **Outlier clipping** may remove legitimate luxury listings, shifting price distributions.
- **Dropping shared rooms** narrows the population and may distort affordability conclusions.  

These risks are documented in the module summary and addressed through careful cleaning decisions and transparent reporting.

---

### **5. How does reproducibility support later ML, DL, generative, and agentic projects?**

Reproducibility ensures that future models and systems can be trained, evaluated, and compared consistently. By pinning dependencies, using version control, and writing modular functions, this workflow becomes a stable foundation for:

- ML model training  
- DL experiments  
- generative model pipelines  
- agentic workflows  

Reproducibility is essential for debugging, collaboration, and long‑term maintainability across the entire capstone.

---

## **Repository Structure**

```
├── data_workflow.ipynb
├── module_summary.pdf
├── requirements.txt
├── README.md
├── data/
|   └── AB_NYC_2019.csv 
└── charts/
    ├── fig_median_price_by_neighbourhood.png
    ├── fig_price_by_property_type_across_neighbourhoods.png
    ├── fig_price_distribution_by_neighbourhood.png
    └── fig_record_distributions.png
```

---

## **License**

This project uses publicly available data from Kaggle. All analysis and code are original work.