### Strengths

- **Simplicity and Interpretability**
    - Model is a weighted sum followed by a threshold; weights map directly to feature importance.
    - Easy to implement and understand, making it a good pedagogical tool.
- **Online and Incremental Learning**
    - Can update weights on a per‐example basis (stochastic updates), which suits streaming or very large datasets.
- **Guaranteed Convergence (Linearly Separable Data)**
    - The perceptron convergence theorem ensures finding a separating hyperplane in a finite number of steps if one exists.
- **Computational Efficiency**
    - Training and inference cost is _O(d)_ per sample (where _d_ is the feature dimension), making it lightweight.
        
### Weaknesses

- **Limited to Linearly Separable Problems**
    - Cannot model non‐linearly separable functions (e.g., XOR), since it defines only a single hyperplane.
- **No Confidence or Probability Estimates**
    - Outputs are binary labels; extensions (e.g., logistic regression) are needed for calibrated probabilities.
- **Sensitivity to Noise and Outliers**
    - Hard margin approach (no slack) can lead to oscillation or poor generalization if data are noisy or nearly non‐separable.
- **No Internal Feature Transformation**
    - Unlike multi‐layer networks, it cannot learn intermediate representations—feature engineering is left entirely to the practitioner.