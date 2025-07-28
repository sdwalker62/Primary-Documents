
|**Strengths**|**Weaknesses**|
|---|---|
|Handles missing data and latent variables naturally via E-step formulation|Only guarantees convergence to a local maximum of the likelihood surface|
|Each iteration is guaranteed not to decrease the data likelihood|Highly sensitive to initialization (e.g., choice of starting parameters)|
|Flexible: can be applied to a wide range of probabilistic models (mixtures, HMMs, etc.)|Requires full specification of model structure and number of components a priori|
|Often straightforward to implement (alternating E and M steps)|Can be computationally intensive—especially in high dimensions or large datasets|
|Tends to converge quickly in early iterations|Convergence slows dramatically near optima (plateauing behavior)|
