# 🌍 Country Segmentation: Unsupervised Learning Project

## Project Overview

This project applies unsupervised learning techniques to segment 167 countries based on socio-economic indicators. The objective is to group countries with similar characteristics and extract data-driven insights. Principal Component Analysis (PCA) was used for dimensionality reduction, preserving 90% of the variance. Clustering was then performed using KMeans, Hierarchical Clustering, DBSCAN, and HDBSCAN to identify meaningful patterns in the data.

---

## 📁 Dataset Summary

The dataset contains the following 10 columns:

| Column Name     | Description                      |
|-----------------|----------------------------------|
| `country`       | Country name                     |
| `child_mort`    | Death of children under 5 years of age per 1000 live births             |
| `exports`       | Exports as a percentage of GDP per capita        |
| `health`        | Health expenditure as a percentage of GDP per capita   |
| `imports`       | Imports as a percentage of GDP per capita         |
| `income`        | Net income per person                |
| `inflation`     | Annual growth rate of total GDP                   |
| `life_expec`    | Average life expectancy at birth, assuming current mortality rates persist                  |
| `total_fer`     | Estimated number of children per woman, based on current age-specific fertility rates                   |
| `gdpp`          | GDP per capita, calculated as total GDP divided by total population                   |


---

## ⚙️ Methodology

### 1. 📉 PCA Dimensionality Reduction
- PCA was applied to the 9 numerical features.
- Based on cumulative explained variance, 3 components were selected.
- The dataset was reduced to 3 dimensions with minimal information loss.

### 2. 📌 KMeans Clustering
- Optimal cluster count was determined using Elbow method, Kneedle algorithm, and evaluation metrics (Silhouette, Calinski-Harabasz, Davies-Bouldin).
- Model was built with 3 clusters.
- Clusters were labeled based on boxplot analysis:
  - `2`: Budget Needed
  - `0`: In Between
  - `1`: No Budget Needed
- Country-level map visualization was created using Plotly.

### 3. 📌 Hierarchical Clustering
- Dendrogram was plotted and various cluster counts were tested.
- Based on scores, 3 clusters were selected.
- Labels were assigned similarly and visualized on a map.

### 4. 📌 DBSCAN
- Multiple combinations of `eps` and `min_samples` were tested.
- Result: 1 noise point and all other data grouped into a single cluster.
- No meaningful segmentation was achieved.

### 5. 📌 HDBSCAN
- After parameter tuning, 4 clusters were formed.
- One cluster consisted of noise points.
- Remaining clusters were labeled via boxplot analysis and visualized on a map.

---

## 🏷️ Cluster Labeling Strategy

Cluster labels were not assigned arbitrarily. Instead, they were derived from **boxplot analysis** of key features such as `income` and `child_mort`. Based on these insights, the following labels were defined:

- **Budget Needed**: Low income and high child mortality
- **In Between**: Moderate income and child mortality
- **No Budget Needed**: High income and low child mortality

---

## 📊 Score Comparison

Each algorithm was applied to both the **original dataset** and the **PCA-reduced dataset**. The results show that PCA-enhanced models consistently performed better:

| Algorithm        | Data Type         | Silhouette | Calinski-Harabasz | Davies-Bouldin |
|------------------|------------------|------------|--------------------|----------------|
| KMeans           | Original          | 0.3398       | 99.3507              | 1.1187           |
| KMeans           | PCA               | **0.4386**   | **169.2469**          | **0.8695**       |
| Hierarchical     | Original          | 0.3163       | 86.4744              | 1.1919           |
| Hierarchical     | PCA               | **0.3983**   | **129.4320**          | **0.8592**       |
| DBSCAN           | Original          | 0.5265       | 4.4292                | 1.9843           |
| DBSCAN           | PCA               | **0.6020**   | **10.0731**            | **0.2785**       |
| HDBSCAN          | Original          | 0.1625       | 27.6699              | 2.0380           |
| HDBSCAN          | PCA               | **0.2401**   | **38.5823**          | **1.8041**       |

---

## ✅ Conclusion

PCA-based dimensionality reduction significantly enhanced clustering performance and interpretability across all algorithms. Post-PCA scores improved consistently across all three metrics.
- KMeans and Hierarchical Clustering produced the most meaningful segmentations, especially after PCA, with high Silhouette and Calinski-Harabasz scores.
- DBSCAN achieved the highest Silhouette score and lowest Davies-Bouldin index after PCA. However, it identified only one cluster plus noise, which limits its segmentation utility. Despite strong scores, the low number of clusters makes interpretation less practical.
- HDBSCAN effectively separated noise and produced multiple meaningful clusters. While its scores were slightly lower than DBSCAN, it offered a more balanced segmentation structure.
In summary, with PCA, KMeans and Hierarchical methods provided strong segmentations, while HDBSCAN excelled in noise handling. DBSCAN, despite high scores, may be less suitable due to its limited cluster output.


---

## 📌 Libraries Used

- `pandas`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `seaborn`
- `plotly`
- `hdbscan`

---
