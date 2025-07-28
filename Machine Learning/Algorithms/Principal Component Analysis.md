
|**Strengths**|**Weaknesses**|
|---|---|
|**Maximum variance capture**Finds orthogonal directions that explain the most variance in the data.|**Linearity assumption**Only captures linear correlations; fails on nonlinear manifolds.|
|**Dimensionality reduction**Projects data to a lower‐dimensional space, reducing computational cost.|**Variance ≠ importance**High‐variance directions may not be the most discriminative for a task.|
|**Noise filtering**By discarding small‐variance components, it can denoise data.|**Sensitive to scaling**Features with larger scales dominate unless data is standardized.|
|**Unsupervised**Requires no labels, making it widely applicable as a preprocessing step.|**Interpretability**Principal components are linear combinations of all features and can be hard to interpret.|
|**Computationally efficient**Well‐optimized SVD algorithms make it scalable to moderately large datasets.|**Outlier sensitivity**Extreme values can skew the computation of principal axes.|
