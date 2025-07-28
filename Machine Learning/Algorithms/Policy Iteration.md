| Strengths                                                                 | Weaknesses                                                                      |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Guaranteed convergence** to the optimal policy in a finite number of iterations (for proper MDPs)                  | **Requires full model** (transition probabilities and rewards)                   |
| **Typically fewer iterations** to converge than Value Iteration (each policy improvement step makes maximal changes) | **Expensive policy evaluation** step (solving a system of linear equations or many sweeps) |
| **Clear separation** of evaluation and improvement phases aids analysis and debugging                               | **Poor scalability** to large or continuous state spaces (curse of dimensionality)      |
| **Basis for extensions** (e.g., Modified Policy Iteration, Approximate PI)                                         | **Synchronous updates** limit applicability in asynchronous or sample-based settings    |
