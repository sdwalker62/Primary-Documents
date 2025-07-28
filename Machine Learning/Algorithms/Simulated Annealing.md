### Strengths

- **Escapes Local Minima**: By occasionally accepting “uphill” moves (worse solutions) with probability $e^{-\Delta E / T}$, it can jump out of local optima rather than getting stuck.
- **Simplicity & Flexibility**: Requires only a problem-specific neighborhood generator and cost function; no gradient information or complex data structures needed.
- **Asymptotic Global Optimality**: With a suitably slow (“logarithmic”) cooling schedule, it is guaranteed to converge to the global optimum as $T\to0$ in infinite time.

### Weaknesses

- **Slow Convergence**: Practical cooling schedules must be much faster than the theoretical ideal, often leading to long runtimes or premature “freezing.”
- **Parameter Sensitivity**: Performance heavily depends on the initial temperature, cooling rate, and neighborhood definition—tuning these can be problem-specific and time-consuming.
- **No Finite-Time Guarantees**: In real applications (finite time), there’s no guarantee of reaching—or even closely approximating—the global optimum.
- **Stochastic Outcomes**: Different runs can yield different solutions; one often needs multiple restarts to assess reliability.
