### Strengths

- **Margin maximization:** Finds the decision boundary with the largest margin, often improving generalization.
- **Kernel trick:** Can handle non-linearly separable data by implicitly mapping inputs into high-dimensional feature spaces (e.g., via RBF, polynomial kernels).
- **Sparsity & memory efficiency:** Only support vectors determine the model, so storage depends on the number of boundary points rather than the entire dataset.
- **Convex optimization:** Global optimum is guaranteed—no local minima issues.
- **Robust in high dimensions:** Performs well when the number of features exceeds the number of samples.
    
### Weaknesses

- **Scalability:** Training time and memory grow super-linearly (often between O(n²) and O(n³)), making large datasets (>10⁴ samples) challenging.
- **Kernel & hyper-parameter selection:** Performance hinges on choosing an appropriate kernel and tuning C (regularization) and kernel-specific parameters, often via costly cross-validation.
- **Non-probabilistic outputs:** Standard SVMs don’t directly yield probability estimates (though methods like Platt scaling can be applied).
- **Sensitivity to noisy/outlier data:** Support vectors can be heavily influenced by mislabeled or noisy points unless properly regularized.
- **Multi-class extension overhead:** Originally binary classifiers; multi-class requires strategies like one-vs-rest or one-vs-one, adding complexity.