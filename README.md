# Fake News Detection — MSc Project

**Student:** Muhammad Anas | **ID:** 25001608
**Supervisor:** Tazeen Syed
**University:** University of Hertfordshire
**Module:** 7COM1040-0509-2025 — Computer Science Masters Project
**Submission:** 1 September 2026

---

## Project Overview

This project investigates whether transformer-based models outperform
traditional machine learning approaches for fake news detection and
whether they generalise better to unseen data.

Two approaches are compared:

| Approach | Models |
|---|---|
| Traditional NLP (Baseline) | Logistic Regression, SVM, Naive Bayes |
| Transformer-Based | DistilBERT (fine-tuned) |

---

## Research Questions

- **RQ1:** Which model achieves higher Macro F1 on the primary test set?
- **RQ2:** Does the transformer model generalise better to unseen data?
- **RQ3:** How do the models compare in explainability and computational cost?
- **RQ4:** What are the risks of deploying fake news classifiers in practice?

---

## Dataset

**Primary:** LIAR Dataset (Wang, 2017)
- 12,836 labelled political statements from PolitiFact
- 6 veracity classes → mapped to binary (Fake / Real)
- Split: 10,269 train / 1,284 val / 1,283 test

**Secondary (Generalisation Test):** FakeNewsNet (Shu et al., 2020)

> Datasets are not included in this repository.
> Download LIAR from: https://www.cs.ucsb.edu/~william/data/liar_dataset.zip
> Place files in: `data/raw/liar/`

---

## Project Structure
Fake-News-Detection/

├── data/

│   ├── raw/                  # Original dataset files (not tracked)

│   └── processed/            # Cleaned CSV files (not tracked)

├── notebooks/

│   └── week1_setup.ipynb     # Week 1 — setup, EDA, preprocessing

├── models/                   # Saved model files (not tracked)

├── results/                  # Charts, confusion matrices, metrics

├── docs/

│   ├── literature_matrix.xlsx

│   └── MSc_Project_Report.docx

├── .gitignore

├── progress_log.md

└── README.md

---

## Setup Instructions

**1. Clone the repository**
```bash
git clone https://github.com/your-username/Fake-News-Detection.git
cd Fake-News-Detection
```

**2. Install dependencies**
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
pip install nltk spacy textstat vaderSentiment
pip install transformers datasets torch accelerate
pip install lime shap streamlit openpyxl
```

**3. Download LIAR dataset**
- Download from the link above
- Place `train.tsv`, `valid.tsv`, `test.tsv` in `data/raw/liar/`

**4. Run the notebook**
```bash
jupyter notebook notebooks/week1_setup.ipynb
```

---

## Weekly Progress

| Week | Focus | Status |
|---|---|---|
| Week 1 | Environment setup, data loading, preprocessing | ✅ Complete |
| Week 2 | TF-IDF features, baseline model training | ⏳ In Progress |
| Week 3 | DistilBERT fine-tuning | 🔲 Pending |
| Week 4 | Generalisation testing | 🔲 Pending |
| Week 5 | Explainability (SHAP, LIME) + demo | 🔲 Pending |
| Weeks 6–11 | Dissertation writing | 🔲 Pending |

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.11 |
| Data | pandas, numpy |
| ML | scikit-learn |
| NLP | nltk, textstat, vaderSentiment |
| Transformer | HuggingFace transformers, PyTorch |
| Explainability | SHAP, LIME |
| Visualisation | matplotlib, seaborn |
| Demo | Streamlit |
| IDE | VS Code + Jupyter |

---

## References

- Wang, W. Y. (2017). LIAR, LIAR Pants on Fire. *ACL 2017*.
- Shu, K. et al. (2017). Fake News Detection on Social Media. *ACM SIGKDD*.
- Sanh, V. et al. (2019). DistilBERT. *arXiv:1910.01108*.
- Devlin, J. et al. (2019). BERT. *NAACL 2019*.

---

*Last updated: Week 1 — June 2026*