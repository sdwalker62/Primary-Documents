### Strengths

- **Simplicity and speed**: Easy to implement; uses a fast, iterative procedure that scales linearly with the number of points and clusters.
- **Scalability**: Handles large datasets efficiently, especially with optimized implementations (e.g., using k-means++ initialization).
- **Interpretability**: Produces explicit cluster centers and assigns each point to exactly one cluster, making results easy to understand.
- **Deterministic (with fixed init)**: If you fix the random seed or use k-means++ deterministically, you get reproducible partitions.

### Weaknesses

- **Predefined k**: You must choose the number of clusters in advance, which may be unknown or hard to estimate.
- **Shape and size assumptions**: Assumes roughly spherical, equal-variance clusters; struggles with non-convex or differently sized/dense clusters.
- **Initialization sensitivity**: Poor initial centroids can lead to suboptimal solutions or slow convergence.
- **Outlier sensitivity**: A single outlier can significantly distort cluster centers.
- **Feature scaling**: Requires careful normalization; variables on larger scales dominate the distance metric.
