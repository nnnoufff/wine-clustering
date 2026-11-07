# Clustering Mini Project: K-Means, DBSCAN and Hierarchical

**Group 6**

Apply three clustering algorithms to the same dataset and compare how they behave.

## Dataset

[Wine dataset](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_wine.html) (from `sklearn`): 178 wines, 13 chemical features, from 3 grape types.

The algorithms never see the grape type. It is used only at the end to check the results (ARI).

## What We Did

1. **Data preparation:** checked for missing values (none) and standardized the features, because all three algorithms use distances. PCA (2 components) is used only to draw the clusters.
2. **K-Means:** chose K = 3 with the Elbow Method.
3. **DBSCAN:** tuned `eps` and `min_samples` over a grid and chose `eps = 2.4`, `min_samples = 5`.
4. **Hierarchical:** compared ward, complete and average linkage; ward had the best silhouette. The dendrogram supports 3 clusters.
5. **Visualization:** side-by-side PCA plots of the three results.
6. **Evaluation and comparison:** cluster shape, number of clusters, sensitivity to noise, Silhouette score and Adjusted Rand Index (ARI).

## Results

| Algorithm | Clusters | Noise points | Silhouette | ARI (vs grape type) |
|---|---|---|---|---|
| K-Means | 3 | 0 | 0.285 | **0.897** |
| DBSCAN | 2 | 36 | 0.327 | 0.421 |
| Hierarchical (ward) | 3 | 0 | 0.277 | 0.790 |

DBSCAN's silhouette looks higher only because its 36 noise points are excluded, so ARI is the fairer comparison.

## Key Insights

- **K-Means performed best** (ARI 0.90). The wine groups are round and similar in size, which is what K-Means expects.
- **Hierarchical** was close (ARI 0.79) and gives a dendrogram that shows how the groups relate.
- **DBSCAN performed worst** (ARI 0.42). The groups touch each other with no clear empty space between them, so it found only 2 clusters.
- The best algorithm depends on the shape of the data.

## When to Use Each Algorithm

| Algorithm | Use when | Strengths | Weaknesses |
|---|---|---|---|
| K-Means | You know or can guess K and the groups are round; large data | Simple, fast | Must choose K, round clusters only, sensitive to outliers |
| DBSCAN | Clusters have unusual shapes, unknown K, or the data has outliers | Finds K by itself, detects noise, any shape | Hard to choose `eps`, weak when densities are similar |
| Hierarchical | Small data, and you want to see how groups are related | Dendrogram shows structure, no random start | Slow on large data |

## How to Run

```bash
pip install pandas matplotlib scikit-learn scipy jupyter
jupyter notebook MiniProject_Group6_Clustering_Wine.ipynb
```

## Files

- `MiniProject_Group6_Clustering_Wine.ipynb`: code, visualizations, explanations and final summary

## Team

Group 6
