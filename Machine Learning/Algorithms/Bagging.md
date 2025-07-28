### Strengths

- **Variance reduction**: By averaging over many bootstrap-resampled models, bagging stabilizes predictions and reduces overfitting for high-variance learners (e.g., deep trees).
- **Parallelizable**: Each base learner is trained independently, so you can distribute the work easily across CPUs or machines.
- **Robustness to noise**: Aggregation tends to dilute the impact of noisy samples or outliers in any single bootstrap dataset.
- **Works “out of the box”**: Requires minimal tuning—apart from the number of base learners, you can often pair bagging with a default estimator (like a decision tree) and see immediate gains.
- **Improved accuracy**: Especially effective when the base learner is unstable; often yields a significant boost over a single model.

### Weaknesses

- **Computational cost**: Training and storing dozens or hundreds of models can be both time- and memory-intensive.
- **No bias reduction**: Bagging averages models but cannot correct a systematically biased base learner.
- **Diminishing returns**: Beyond a certain number of learners, additional models add little new information yet still incur cost.
- **Interpretability**: The ensemble obscures individual decision paths, making it harder to inspect how predictions are made.
- **Data hungry**: Each bootstrap sample leaves out about 37% of the data (“out-of-bag”); with small datasets, this can reduce each learner’s effective training set.