# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Scaler "FlipItNews" NLP business case. The deliverable is a single Jupyter notebook (`EDA.ipynb`) that performs EDA, text preprocessing, vectorization, and multi-class classification on news articles, then is exported to PDF for submission. This is a coursework repo, not a package — there is no build, no test suite, no lint config, and no `requirements.txt`. All work happens inside the notebook.

## Files

- `flipitnews-data.csv` — dataset, 2225 rows, two columns: `Category`, `Article`. Categories are `Business`, `Entertainment`, `Politics`, `Sports`, `Technology`.
- `EDA.ipynb` — the working notebook (currently empty).
- `Business Case _ NLP FlipItNews Approach.pdf` — the brief. Defines required sections, expected models, and the questionnaire that must be answered in the final notebook.
- `NLP FlipItNews.docx` — supplementary brief (same content as PDF).

## Required scope (from the brief)

The notebook is expected to cover, in order:

1. **EDA** — shape/info/describe, category distribution (count plot), article length stats, common words per category.
2. **Preprocessing** — deduplicate, missing-value check, remove non-letters and stopwords, tokenize, lemmatize.
3. **Feature engineering** — Bag of Words **and** TF-IDF vectorization, compared.
4. **Modeling** — at least three models for multi-class classification. The brief explicitly names Naive Bayes, Decision Tree / Random Forest, and K-Nearest Neighbors as the comparison set. Use a 75:25 train-test split (stratified by category).
5. **Evaluation** — accuracy, precision, recall, F1, confusion matrix, per-category performance. Use macro-averaged metrics since the dataset is mildly imbalanced.
6. **Questionnaire** — answer the 9 questions at the end of the PDF inside the notebook (count of articles, dominant category, count of Technology articles, stopwords definition, stemming vs. lemmatization, BoW vs. TF-IDF, train/test shapes after 75:25 split, best model, precision/recall trade-off).

## Running the notebook

```powershell
jupyter notebook EDA.ipynb
```

Expected stack: `pandas`, `numpy`, `matplotlib`, `seaborn`, `nltk` (stopwords + WordNetLemmatizer — requires `nltk.download('stopwords')`, `nltk.download('wordnet')`, `nltk.download('omw-1.4')`), `scikit-learn` (`CountVectorizer`, `TfidfVectorizer`, `train_test_split`, `MultinomialNB`, `RandomForestClassifier`, `KNeighborsClassifier`, `classification_report`, `confusion_matrix`). `wordcloud` is optional but commonly used for the per-category visuals.

## Conventions for this notebook

- The dataset path is relative: `pd.read_csv('flipitnews-data.csv')`. Keep it that way — the notebook is exported to PDF and shared as-is.
- Article text is already lowercased in the source CSV; preprocessing still needs to strip non-letters, stopwords, and lemmatize.
- When splitting, pass `stratify=y` — class counts are uneven (Sports/Business are over-represented relative to Technology/Entertainment) and the questionnaire asks for the Technology count specifically.
- After completing the notebook, export to PDF via Chrome's Print dialog (per the brief's submission instructions), not via `nbconvert` — the brief mandates the Chrome-print path.
