
| Strengths                                                                                 | Weaknesses                                                                                                          |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Guaranteed convergence** to the optimal value function under standard DP assumptions.   | **Model requirement:** Needs full knowledge of transition probabilities and rewards.                                |
| **Conceptual simplicity:** Easy to implement as a synchronous dynamic-programming update. | **Scalability issues:** Suffering from the curse of dimensionality in large state spaces.                           |
| **Global updates:** Computes values for all states, enabling broad policy insights.       | **Computationally expensive:** Iterative sweeps over all states until convergence.                                  |
| **Monotonic improvement:** Value function improves (or stays same) each iteration.        | **Slow convergence:** Especially near the optimal threshold and for small discount factors.                         |
| **Parallelizable:** State updates can be distributed across processors.                   | **Memory intensive:** Must store a value for every state; intractable for continuous domains without approximation. |
