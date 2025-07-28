
|**Strengths**|**Weaknesses**|
|---|---|
|• **On-policy learning**: Evaluates and improves the exact behavior policy (including exploration), yielding tighter policy–value coupling.|• **Sample inefficiency**: Requires many interactions to accurately estimate action values, leading to slower learning.|
|• **Robust to overestimation bias**: Because it uses actual next actions, it avoids the optimistic bias inherent in max-based updates.|• **Slower convergence**: Often converges more slowly than off-policy methods like Q-learning, especially when ε is large.|
|• **Converges under standard conditions**: Proven to converge to the optimal policy in the limit, given a decaying exploration schedule.|• **Sensitive to exploration strategy**: Poorly tuned ε-greedy or softmax policies can trap SARSA in suboptimal behavior.|
|• **Naturally adapts to non-stationary environments**: Continuously updates as the policy evolves, without requiring separate evaluation.|• **Tied to behavior policy**: Cannot easily evaluate or learn about policies other than the one currently being executed (limited off-policy use).|
|• **Simple algorithmic structure**: Easy to implement and extend (e.g., to function approximation).|• **High variance**: On-policy updates can exhibit greater variance when exploration causes erratic action choices.|