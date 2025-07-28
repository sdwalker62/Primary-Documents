
### Strengths

- **Reduced Bias:** Sequentially focuses on hard-to-predict examples, producing a strong learner from weak base models.
- **Flexibility:** Can work with many types of base learners (e.g., decision stumps, trees) and loss functions.
- **High Accuracy:** Often outperforms single models and bagging on clean datasets by combining many weak predictors.
    
#### Weaknesses

- **Overfitting Risk:** Can fit noise and outliers if run with too many iterations or on very noisy data.
- **Sensitivity to Noise:** Mistakes in early rounds get amplified, making it less robust when labels are noisy.
- **Sequential Dependency:** Each model depends on the previous, limiting parallelization and increasing training time.