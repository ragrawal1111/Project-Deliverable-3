# Deliverable 3: Classification, Clustering, and Pattern Mining

Course: MSCS-634 — Advanced Big Data and Data Mining
Author: Rajiv Agrawal
Date: 19 April 2026

**Dataset:** UCI Wine Quality (white wine) — 4,898 samples, 11 physicochemical features, binary quality label (good ≥ 6 / bad < 6).

---

## Key Insights

### Classification
- Three models were trained: **Decision Tree**, **K-Nearest Neighbors (KNN)**, and **Support Vector Machine (SVM)**.
- The tuned SVM (via `GridSearchCV` over `C`, `gamma`, and `kernel`) achieved the highest accuracy (~80%) and best F1 score.
- ROC curves show SVM and KNN both achieve AUC > 0.80, significantly outperforming a random classifier.
- Confusion matrices reveal that false negatives (good wines predicted as bad) are the primary error type across all models.

### Clustering
- K-Means with **k=3** produced three distinct wine segments based on physicochemical profiles:
  - **Cluster A (high alcohol, low residual sugar):** Dry, higher-quality wines.
  - **Cluster B (high residual sugar, low alcohol):** Sweet, lower-quality wines.
  - **Cluster C (moderate values):** Mid-tier wines with balanced properties.
- PCA-based 2D visualization confirms meaningful separation between clusters.

### Association Rule Mining
- Apriori identified frequent itemsets with `min_support=0.1` and derived rules with `min_confidence=0.5`.
- Notable patterns: *high alcohol → low density* (physicochemical relationship); *low residual sugar + high alcohol → good quality*.
- These rules are consistent with domain knowledge about wine fermentation chemistry.

---

## Practical Relevance

- **Classification models** enable wine producers and distributors to predict quality from measurable physicochemical properties before formal tasting panels, reducing cost and time.
- **Clustering** segments wine inventory for targeted marketing — e.g., promoting high-alcohol dry wines to enthusiasts, or sweet wines to casual drinkers — and can guide pricing strategies.
- **Association rules** provide actionable production guidelines: winemakers can optimize fermentation to hit target alcohol levels and residual sugar ranges associated with higher quality outcomes. Retailers can also use these patterns to build recommendation engines.

---

## Challenges and How They Were Addressed

| Challenge | Solution |
|---|---|
| Class imbalance (more "good" wines than "bad") | Evaluated with F1 score and confusion matrix rather than accuracy alone |
| Choosing k for K-Means | Selected k=3 to reflect low/medium/high quality tiers; cluster means validated the choice |
| High-dimensional data for visualization | Applied PCA (2 components) for 2D scatter plot of cluster assignments |
| Sparse frequent itemsets for Apriori | Lowered `min_support` to 0.1 to surface sufficient rules while keeping them meaningful |