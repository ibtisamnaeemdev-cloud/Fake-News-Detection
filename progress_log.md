# Progress Log — Fake News Detection MSc Project

**Student:** Muhammad Anas    | **ID:** 25001608
**Supervisor:** Tazeen Syed   | **University:** University of Hertfordshire
**Module:** 7COM1040-0509-2025

---

## Week 1 — 11 June 2026 to 17 June 2026

**Status:** ✅ Complete
**Supervisor Meeting:** 18 June 2026

---

### Goals Set for This Week

- Set up the full development environment
- Download and load the LIAR dataset
- Perform initial data exploration
- Clean and preprocess the data
- Start the literature matrix
- Set up GitHub repository

---

### Tasks Completed

#### 1. Development Environment Setup
- Installed Python 3.11, VS Code, and Jupyter Notebook
- Installed all required libraries: pandas, numpy, scikit-learn, nltk, textstat, vaderSentiment, transformers, torch, datasets, matplotlib, seaborn, streamlit, lime, shap, openpyxl
- Ran environment verification script — all imports successful
- Confirmed PyTorch installed (CPU mode; GPU not available locally)

#### 2. Project Folder Structure Created
```
Fake-News-Detection/
├── data/
│   ├── raw/
│   │   ├── liar/          ← LIAR dataset TSV files
│   │   └── fakenewsnet/   ← FakeNewsNet files
│   └── processed/         ← cleaned CSV outputs
├── notebooks/
├── models/
├── results/
└── docs/
```

#### 3. LIAR Dataset Loaded
- Downloaded train.tsv, valid.tsv, test.tsv from official GitHub source
- Placed in `data/raw/liar/`
- Loaded into Pandas DataFrames with all 14 columns correctly named
- Confirmed record counts: 10,269 train / 1,284 validation / 1,283 test = **12,836 total**

#### 4. Data Exploration
- Explored all 6 veracity labels: pants-fire, false, barely-true, half-true, mostly-true, true
- Checked label distribution — reasonably balanced across classes
- Explored speaker, party, subject, and context columns
- Generated and saved label distribution bar chart to `results/label_distribution.png`

#### 5. Binary Label Mapping
- Mapped 6 original labels to binary classification:
  - `0 = FAKE` → pants-fire, false, barely-true
  - `1 = REAL` → half-true, mostly-true, true
- Added `binary_label` column to all three DataFrames
- Confirmed class balance: approximately 50/50 split

#### 6. Text Cleaning Pipeline
- Implemented `clean_text()` function with the following steps:
  1. Lowercase conversion
  2. Punctuation and special character removal (regex)
  3. Extra whitespace removal
  4. NLTK stopword removal
  5. Result stored in `clean_text` column
- Applied to train, validation, and test sets
- Original `statement` column preserved for DistilBERT use later

#### 7. Cleaned Data Saved
- Saved all three cleaned DataFrames to `data/processed/`:
  - `train_cleaned.csv` — 10,269 rows
  - `val_cleaned.csv` — 1,284 rows
  - `test_cleaned.csv` — 1,283 rows

# 8. Literature Matrix Started (`docs/literature_matrix.xlsx`)
- Created 4-sheet Excel workbook:
  - **Sheet 1 — Literature Matrix:** main research database (8 columns)
  - **Sheet 2 — Paper Notes:** detailed summaries for dissertation writing
  - **Sheet 3 — Quick Reference:** paper → chapter section mapping
  - **Sheet 4 — Reading Tracker:** progress towards 20-paper target
- Entered 6 papers with full details:

| # | Paper | Type |
|---|---|---|
| 1 | Wang (2017) — LIAR Dataset | Dataset |
| 2 | Shu et al. (2017) — Fake News Survey | Traditional NLP |
| 3 | Potthast et al. (2018) — Stylometric Inquiry | Traditional NLP |
| 4 | Devlin et al. (2019) — BERT | Transformer |
| 5 | Sanh et al. (2019) — DistilBERT | Transformer |
| 6 | Thorne et al. (2018) — FEVER Dataset | Dataset |

#### 9. Dissertation Report Started
- Created full MSc report skeleton (Word document) with all 7 chapters
- Wrote complete **Chapter 1: Introduction** including:
  - 1.1 Background
  - 1.2 Problem Statement
  - 1.3 Research Gap
  - 1.4 Aim of the Study
  - 1.5 Research Questions (RQ1–RQ4)
  - 1.6 Chapter Summary

#### 10. GitHub Repository Setup
- Created repository: `Fake-News-Detection`
- Added `.gitignore` to exclude `data/raw/`, `data/processed/`, `models/` from version control
- Committed and pushed: notebooks, docs, results, .gitignore
- Issue encountered: 33,047 FakeNewsNet files staged accidentally → resolved with `git rm -r --cached data/`

---

### Problems Encountered

| Problem | How Resolved |
|---|---|
| FakeNewsNet (33k files) accidentally staged in Git | Added `.gitignore`, ran `git rm -r --cached data/`, recommitted |
| TSV files had no column headers | Manually assigned 14 column names from README |
| NLTK punkt tokenizer missing | Ran `nltk.download('punkt')` and `nltk.download('punkt_tab')` |

---

### Files Produced This Week

| File | Location | Description |
|---|---|---|
| `week1_setup.ipynb` | `notebooks/` | Main notebook — all 7 cells complete |
| `train_cleaned.csv` | `data/processed/` | 10,269 cleaned training records |
| `val_cleaned.csv` | `data/processed/` | 1,284 cleaned validation records |
| `test_cleaned.csv` | `data/processed/` | 1,283 cleaned test records |
| `label_distribution.png` | `results/` | Bar chart of 6-class label counts |
| `literature_matrix.xlsx` | `docs/` | 4-sheet literature tracking spreadsheet |
| `MSc_Project_Report.docx` | `docs/` | Full report skeleton + Chapter 1 written |
| `progress_log.md` | root | This file |

---

### Hours Logged

| Activity | Estimated Hours |
|---|---|
| Environment setup & verification | 1.5 hrs |
| Dataset download, loading, exploration | 2.0 hrs |
| Data cleaning & preprocessing | 1.5 hrs |
| Literature reading (6 papers) | 3.0 hrs |
| Literature matrix creation | 1.5 hrs |
| Chapter 1 writing | 2.0 hrs |
| GitHub setup & fixing issues | 1.0 hr |
| **Total** | **12.5 hrs** |

---

### Key Decisions Made This Week

1. **Binary classification chosen over 6-class** — simplifies the task and is consistent with majority of literature; makes results easier to interpret and compare
2. **Local TSV files used instead of Hugging Face** — gives full control over data, works offline, supervisor can inspect raw files directly
3. **DistilBERT chosen over full BERT** — 40% smaller, 60% faster, retains 97% performance; more practical for comparison with traditional models (RQ3)
4. **Macro F1 as primary metric** — treats both classes equally regardless of any class imbalance; more informative than accuracy alone

---

### Plan for Week 2

- [ ] Build TF-IDF vectoriser on training set
- [ ] Extract handcrafted features: article length, punctuation ratio, readability score (Flesch), VADER sentiment
- [ ] Train Logistic Regression — evaluate on test set
- [ ] Train SVM (RBF kernel) — evaluate on test set
- [ ] Train Naive Bayes — evaluate on test set
- [ ] Generate confusion matrix for each baseline model
- [ ] Compile results table: accuracy, precision, recall, Macro F1 for all 3 models
- [ ] Read 3 more papers for literature matrix (LIME, SHAP, FakeNewsNet paper)
- [ ] Begin drafting Chapter 2: Literature Review

---

## Week 2 — 18 June 2026 to 24 June 2026

**Status:** ✅ Complete
**Supervisor Meeting:** [insert date]

---

### Goals Set for This Week

- Build TF-IDF feature pipeline
- Train 3 baseline models: Logistic Regression, SVM, Naive Bayes
- Generate confusion matrices for each model
- Evaluate using Accuracy, Precision, Recall, Macro F1
- Add 5 new papers to literature matrix (LIME, SHAP, FakeNewsNet, 2 surveys)
- Continue dissertation writing

---

### Tasks Completed

#### 1. TF-IDF Feature Extraction
- Reloaded cleaned data from `data/processed/`
- Dropped rows where `clean_text` was empty/NaN after Week 1 stopword removal — **29 rows dropped from train (10,269 → 10,240), 16 rows dropped from test (1,283 → 1,267)**, validation set unaffected (1,284 → 1,284)
- Built `TfidfVectorizer` with `max_features=5000`, `ngram_range=(1,2)`, `min_df=2`, `max_df=0.9`
- Fitted on training set, transformed train/val/test splits
- Confirmed vocabulary size: **5,000 terms**
- Saved fitted vectoriser to `models/tfidf_vectorizer.pkl`

#### 2. Baseline Model Training
- Trained three classifiers on TF-IDF features:
  - Logistic Regression (`max_iter=1000`)
  - Linear SVM (`LinearSVC`, `max_iter=2000`)
  - Multinomial Naive Bayes
- All three trained successfully with no convergence errors
- Saved trained models to `models/logistic_regression.pkl`, `models/linear_svm.pkl`, `models/naive_bayes.pkl`

#### 3. Validation Set Evaluation

| Model | Accuracy | Macro F1 | Macro Precision | Macro Recall |
|---|---|---|---|---|
| **Logistic Regression** | **0.6168** | **0.6063** | **0.6210** | 0.6112 |
| Linear SVM | 0.6044 | 0.6014 | 0.6035 | 0.6019 |
| Naive Bayes | 0.6121 | 0.5999 | 0.6170 | 0.6061 |

- 🏆 **Best baseline model: Logistic Regression** (highest Macro F1 = 0.6063)
- Per-class pattern consistent across all three models: precision/recall for the **Fake** class noticeably weaker than for **Real** (e.g. LR: Fake recall 0.47 vs Real recall 0.75) — models are biased toward predicting Real, flagged as a key limitation to investigate in Week 3

#### 4. Confusion Matrices
- Generated and saved side-by-side confusion matrices for all 3 models (validation set) to `results/baseline_confusion_matrices.png`
- Generated Macro F1 comparison bar chart to `results/baseline_f1_comparison.png`

#### 5. Final Test Set Evaluation (RQ1 Baseline Answer)
- Ran best model (Logistic Regression) on held-out test set:

| Metric | Score |
|---|---|
| Accuracy | 0.6180 |
| Macro F1 | 0.5973 |
| Macro Precision | 0.6089 |
| Macro Recall | 0.5989 |

- Fake class: precision 0.58, recall 0.45, f1 0.51 (support 553)
- Real class: precision 0.64, recall 0.75, f1 0.69 (support 714)
- Saved as `results/baseline_best_model_test_result.json` — this is the baseline figure DistilBERT must beat to answer RQ1

#### 6. Literature Matrix Expanded
- Added 5 new papers to `docs/literature_matrix.xlsx` (Literature Matrix, Paper Notes, and Quick Reference sheets), moving them from "Pending" to "Read" in the Reading Tracker:

| # | Paper | Type |
|---|---|---|
| 7 | Ribeiro et al. (2016) — LIME | Explainability |
| 8 | Lundberg & Lee (2017) — SHAP | Explainability |
| 9 | Zhou & Zafarani (2020) — Fake News Survey | Traditional NLP / Survey |
| 10 | Pérez-Rosas et al. (2018) — Fake News Automatic Detection | Traditional NLP |
| 11 | Shu et al. (2020) — FakeNewsNet | Dataset |

- Reading progress now **11 of 20 papers (55%)**

---

### Problems Encountered

| Problem | How Resolved |
|---|---|
| 29 train rows and 16 test rows had empty `clean_text` after Week 1 stopword removal (statement was entirely stopwords/short) | Dropped via `dropna()` before vectorising; documented row count change |
| All three baseline models plateau around 60% Macro F1 — much lower than hoped | Not a bug — genuine finding. Flagged for Week 3 discussion; possible causes: short statement length limits TF-IDF signal, lack of handcrafted stylometric features (length, sentiment, readability) not yet added, no class weighting applied |
| Models under-predict the Fake class (lower recall) vs Real class | Documented as a limitation; candidate fixes for later: `class_weight='balanced'`, threshold tuning, oversampling |

---

### Files Produced This Week

| File | Location | Description |
|---|---|---|
| `week2_baseline_models.ipynb` | `notebooks/` | TF-IDF + 3 baseline models, evaluation, confusion matrices |
| `tfidf_vectorizer.pkl` | `models/` | Fitted TF-IDF vectoriser (5,000 features) |
| `logistic_regression.pkl` | `models/` | Trained Logistic Regression model |
| `linear_svm.pkl` | `models/` | Trained Linear SVM model |
| `naive_bayes.pkl` | `models/` | Trained Naive Bayes model |
| `baseline_confusion_matrices.png` | `results/` | Confusion matrices for all 3 models (validation) |
| `baseline_f1_comparison.png` | `results/` | Macro F1 comparison bar chart |
| `baseline_validation_results.csv` | `results/` | Validation metrics table for all 3 models |
| `baseline_best_model_test_result.json` | `results/` | Logistic Regression test set result (RQ1 baseline) |
| `literature_matrix.xlsx` | `docs/` | Updated with 5 new papers (11 total) |
| `Week 2 Progress Report.docx` | `docs/` | Formal supervisor report for Week 2 |
| `progress_log.md` | root | This file |

---

### Hours Logged

| Activity | Estimated Hours |
|---|---|
| TF-IDF pipeline build & debugging | 1.5 hrs |
| Training & evaluating 3 baseline models | 2.0 hrs |
| Confusion matrices & comparison charts | 1.0 hr |
| Literature reading (5 papers) | 3.0 hrs |
| Literature matrix update | 1.0 hr |
| Progress report & log writing | 1.5 hrs |
| **Total** | **10.0 hrs** |

---

### Key Decisions Made This Week

1. **TF-IDF with bigrams (1,2) and 5,000 max features** — captures short political phrases (e.g. "not true") that unigrams alone would miss, while keeping the feature space manageable for classical models
2. **Macro F1 confirmed as the headline metric** — the Fake/Real recall gap observed this week makes accuracy alone misleading; Macro F1 will be reported as the primary number throughout the dissertation
3. **Logistic Regression selected as the baseline-to-beat** — best Macro F1 of the three; its test score (0.5973) is the number DistilBERT must outperform to give a positive answer to RQ1
4. **Modest baseline performance treated as a finding, not a failure** — ~60% Macro F1 on a binary task is a legitimate result worth analysing rather than something to hide; will motivate Week 3's handcrafted-feature addition and the transformer comparison

---

### Plan for Week 3

- [ ] Add handcrafted features (article length, punctuation ratio, Flesch readability, VADER sentiment) and re-test baselines with combined feature set
- [ ] Investigate Fake-class recall gap — try `class_weight='balanced'` on LR and SVM
- [ ] Begin DistilBERT fine-tuning: tokenisation, train/val loop, GPU setup (Colab)
- [ ] Run DistilBERT on same test set for direct RQ1 comparison against Logistic Regression baseline (Macro F1 = 0.5973)
- [ ] Read 3 more papers (distribution shift / domain adaptation, for RQ2)
- [ ] Draft Chapter 2: Literature Review using completed literature matrix
- [ ] Draft Chapter 3: Methodology (TF-IDF config, model choices, evaluation strategy)

---

*Log maintained by Muhammad Anas — updated every week on completion*
## Week 3 — 25 June 2026 to 1 July 2026

**Status:** ✅ Complete (Technical) | ⚠️ Partial (Writing — carried to Week 4)
**Supervisor Meeting:** [insert date]

---

### Goals Set for This Week

- Add handcrafted features + re-test baselines
- Investigate Fake-class recall gap (class_weight balanced)
- DistilBERT fine-tuning on Google Colab (GPU)
- Run DistilBERT on test set (RQ1 answer)
- Read 3 papers (distribution shift / domain adaptation)
- Draft Chapter 2: Literature Review
- Draft Chapter 3: Methodology

---

### Tasks Completed

#### 1. Handcrafted Feature Engineering (Part A — Local PC)
- Extracted 10 stylometric features from original `statement` column:
  - `word_count`, `char_count`, `punct_ratio`, `exclamation`
  - `caps_ratio`, `flesch_score` (readability)
  - `vader_pos`, `vader_neg`, `vader_compound` (sentiment)
  - `question_marks`
- Combined TF-IDF (5,000 features) + handcrafted (10 features) = **5,010 total features** using `scipy.sparse.hstack`

#### 2. Class Imbalance Fix — class_weight='balanced'
- Re-trained Logistic Regression with `class_weight='balanced'` and `max_iter=3000`, `solver='lbfgs'`
- Re-trained SVM with `class_weight='balanced'` and `max_iter=10000`
- **Fake class F1 improved significantly: 0.5419 → 0.6002 (+0.0583)**
- Expected Real class trade-off observed: 0.6707 → 0.6190

#### 3. Validation Set Comparison (Week 2 vs Week 3)

| Model | MacroF1 | FakeF1 | RealF1 |
|---|---|---|---|
| Week2 LR (TF-IDF only) | 0.6063 | 0.5419 | 0.6707 |
| **Week3 LR (TF-IDF+HC+Bal)** | **0.6096** | **0.6002** | **0.6190** |
| Week2 SVM (TF-IDF only) | 0.6014 | 0.5673 | 0.6356 |
| Week3 SVM (TF-IDF+HC+Bal) | 0.5930 | 0.5797 | 0.6063 |

#### 4. Week 3 Part A — Test Set Results

| Metric | Score |
|---|---|
| Accuracy | 0.6133 |
| Macro F1 | 0.6085 |
| Fake F1 | 0.57 |
| Real F1 | 0.65 |

- Improvement over Week 2 baseline: **+0.0112**

#### 5. DistilBERT Fine-Tuning (Part B — Google Colab T4 GPU)
- Enabled T4 GPU on Google Colab
- Loaded `distilbert-base-uncased` from Hugging Face
- Built PyTorch `Dataset` and `DataLoader` (batch size = 32)
- Training configuration:
  - Epochs: 4 | Learning rate: 2e-5 | Warmup steps: 100
  - Optimizer: AdamW | Scheduler: Linear warmup
- Training time: ~7.5 minutes total (4 epochs)
- Best model saved at **Epoch 3** (Val F1: 0.6349)
- Epoch 4 showed overfitting (Val Loss increased: 0.684 → 0.739)

#### 6. Training History

| Epoch | Train Loss | Train F1 | Val Loss | Val F1 |
|---|---|---|---|---|
| 1 | 0.6640 | 0.5644 | 0.6511 | 0.6200 |
| 2 | 0.6079 | 0.6593 | 0.6588 | 0.6207 |
| **3** | **0.5216** | **0.7390** | **0.6841** | **0.6349** ← Best |
| 4 | 0.4333 | 0.8015 | 0.7396 | 0.6321 |

#### 7. DistilBERT — Final Test Set Results (RQ1 ANSWERED)

| Metric | Score |
|---|---|
| Accuracy | 0.6448 |
| **Macro F1** | **0.6313** |
| Fake: Precision / Recall / F1 | 0.61 / 0.52 / 0.56 |
| Real: Precision / Recall / F1 | 0.67 / 0.74 / 0.70 |

```
RQ1 FINAL ANSWER:
Logistic Regression (Week 2) : 0.5973
DistilBERT          (Week 3) : 0.6313
Difference                   : +0.0340

✅ DistilBERT outperforms Traditional ML by 0.0340 Macro F1
```

---

### Tasks Carried Forward to Week 4

| Task | Reason |
|---|---|
| Read 3 papers (domain adaptation/distribution shift) | Week 4 has RQ2 generalisation — papers more relevant then |
| Draft Chapter 2: Literature Review | Waiting for Week 4 papers before writing |
| Draft Chapter 3: Methodology | Will write after all experiments complete |

---

### Problems Encountered

| Problem | How Resolved |
|---|---|
| Data files loaded in wrong order (train/test swapped) | Fixed file paths — verified row counts with assert statements |
| LR ConvergenceWarning with lbfgs 1000 iterations | Increased max_iter to 3000 — warning resolved |
| saga solver gave worse results (F1 dropped to 0.51) | Reverted to lbfgs — saga not suitable for sparse TF-IDF data |
| SVM ConvergenceWarning | Increased max_iter to 10000 — resolved |
| Colab showing CPU instead of GPU | Changed Runtime type to T4 GPU and restarted session |
| HuggingFace token warning in Colab | Ignored — public models don't require token |
| UNEXPECTED/MISSING weights in DistilBERT load | Normal behaviour — classification head newly initialised |
| DistilBERT overfitting at Epoch 4 | Best model saved at Epoch 3 based on Val F1 |

---

### Files Produced This Week

| File | Location | Description |
|---|---|---|
| `week3_baseline_improved.ipynb` | `notebooks/` | Part A — Handcrafted features + improved baselines |
| `week3_distilbert_colab.ipynb` | `notebooks/` | Part B — DistilBERT fine-tuning (Colab) |
| `lr_improved.pkl` | `models/` | LR with handcrafted features + balanced weights |
| `svm_improved.pkl` | `models/` | SVM with handcrafted features + balanced weights |
| `distilbert_best/` | `models/` (Google Drive) | Best DistilBERT checkpoint (Epoch 3, 268MB) |
| `distilbert_training_curves.png` | `results/` | Loss + F1 curves across 4 epochs |
| `week3_final_comparison.png` | `results/` | All 5 models Macro F1 bar chart |
| `distilbert_test_results.json` | `results/` | DistilBERT test results + RQ1 answer |
| `week3_results.json` | `results/` | Week 3 Part A test results |

---

### Hours Logged

| Activity | Estimated Hours |
|---|---|
| Handcrafted feature engineering | 1.5 hrs |
| Model training + debugging (solver issues) | 2.0 hrs |
| Colab setup + GPU configuration | 0.5 hrs |
| DistilBERT training (4 epochs) | 0.5 hrs (automated) |
| Results analysis + charts | 1.0 hr |
| Progress log writing | 1.0 hr |
| **Total** | **6.5 hrs** |

---

### Key Decisions Made This Week

1. **class_weight='balanced' adopted permanently** — Fake class recall improvement (+13%) justifies the small Real class trade-off; more honest evaluation for real-world fake news detection
2. **lbfgs solver kept over saga** — Despite saga being recommended for large datasets, lbfgs gave significantly better results on sparse TF-IDF features; convergence warning acceptable at max_iter=3000
3. **Best DistilBERT model = Epoch 3** — Epoch 4 showed clear overfitting (Val Loss increased while Train F1 hit 0.80); saving best by Val F1 was correct strategy
4. **Handcrafted features gave marginal overall improvement** — genuine finding: LIAR's short statements (avg 17 words) limit stylometric signal; documented as dissertation finding not a failure
5. **3 pending tasks carried to Week 4** — literature reading and dissertation writing logically aligned with Week 4's generalisation experiments

---

### Plan for Week 4

- [ ] Read 3 papers on domain adaptation / distribution shift (RQ2)
- [ ] Update literature matrix (14/20 papers target)
- [ ] Set up FakeNewsNet PolitiFact subset for cross-domain testing
- [ ] Run both LR Improved + DistilBERT on FakeNewsNet (RQ2 answer)
- [ ] Measure and document performance drop across domains
- [ ] Draft Chapter 2: Literature Review
- [ ] Draft Chapter 3: Methodology

---

*Log maintained by Muhammad Anas — updated every week on completion*