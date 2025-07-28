
### Strengths

- **Ability to detect arbitrary shapes**: Captures non-convex or elongated clusters since it links on nearest neighbors rather than cluster centroids.
- **No need for initial cluster count**: Produces a full dendrogram; you can choose the number of clusters (or distance threshold) after inspection.
- **Deterministic and parameter-light**: Only requires a distance measure and linkage criterion—no random initialization.
- **Incremental updates**: Easy to update when new data points arrive, by computing distances to existing clusters.

### Weaknesses

- **Chaining effect**: Tends to form long “chains” of points—linking clusters by single bridges—even if overall clusters are well separated.
- **Sensitive to noise and outliers**: A single aberrant point can merge disparate clusters prematurely.
- **Difficulty with varying densities**: Struggles when true clusters have very different point densities; sparse connections dominate merges.
- **Lack of robustness to metric choice**: Results can change substantially with different distance measures; no built-in way to weight cluster compactness.