### Strengths

- **Simplicity**:
    - Easy to implement—just repeatedly propose random moves and accept improvements.
    - No need for gradient information or complex update rules.
- **Low Overhead**:
    - Minimal memory and computation per step; only the current solution and its value need to be stored.
- **Flexibility**:
    - Applicable to any black-box objective (discrete or continuous) as long as you can evaluate candidate solutions.
- **Fast Initial Progress**:
    - Quickly ascends steep gradients in well-behaved regions, often finding a decent solution in few iterations.

### Weaknesses

- **Local Optima**:
    - Tends to get trapped in local maxima/minima; without restarts or diversification, it may never find the global optimum.
- **Step-Size Sensitivity**:
    - Fixed step sizes can be too large (overshoot peaks) or too small (slow convergence).
    - Adaptive schemes add complexity.
- **Plateaus and Ridges**:
    - Struggles on flat regions (no improvement) and narrow ridges (hard to align moves), leading to long stagnation.
- **Scaling Issues**:
    - In high-dimensional spaces, random proposals rarely improve the solution—search becomes inefficient.
- **No Guarantee of Optimality**:
    - Unlike some global methods, there’s no convergence proof to the global optimum; performance depends heavily on restart strategy and problem structure.