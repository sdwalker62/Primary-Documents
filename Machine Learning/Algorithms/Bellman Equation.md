Here’s a structured, graduate-level walkthrough of the Bellman equation in the context of Markov Decision Processes (MDPs).

---

## **1. Setup: Markov Decision Processes**

An MDP is defined by the tuple $(\mathcal{S}, \mathcal{A}, P, R, \gamma)$, where
- $\mathcal{S}$: set of states
- $\mathcal{A}$: set of actions
- $P(s{\prime} \mid s,a)$: transition probability from s to s{\prime} under action a
- $R(s,a)$: expected immediate reward for taking action a in state s
- $\gamma\in[0,1)$: discount factor

The goal is to find a policy $\pi(a\mid s)$ maximizing expected discounted return.

---

## **2. State–Value and Action–Value Functions**

- **State–value** under policy $\pi$:
    $V^{\pi}(s) \;=\; \mathbb{E}{\pi}\biggl[\sum{t=0}^{\infty}\gamma^{t}R_{t+1}\,\big\vert\,S_{0}=s\biggr]$.
- **Action–value** under \pi:
    $Q^{\pi}(s,a) \;=\; \mathbb{E}{\pi}\biggl[\sum{t=0}^{\infty}\gamma^{t}R_{t+1}\,\big\vert\,S_{0}=s,\,A_{0}=a\biggr]$.
    
---

## **3. Bellman Expectation Equation**

In words, the value of a state is the immediate reward plus the discounted value of successor states under the policy. Formally:

$V^{\pi}(s) = \sum_{a}\pi(a\mid s)\Bigl[R(s,a) + \gamma\sum_{s{\prime}}P(s{\prime}\mid s,a)\,V^{\pi}(s{\prime})\Bigr]$.

Similarly for $Q$-values:

$Q^{\pi}(s,a) = R(s,a) + \gamma\sum_{s{\prime}}P(s{\prime}\mid s,a)\sum_{a{\prime}}\pi(a{\prime}\mid s{\prime})\,Q^{\pi}(s{\prime},a{\prime})$.


> **Interpretation:** These are a set of linear equations in the unknowns $\{V^{\pi}(s)\}$ (or $\{Q^{\pi}(s,a)\}$), which—not coincidentally—you can solve (for finite MDPs) via dynamic programming (policy evaluation).

---

## **4. Bellman Optimality Equation**

To find the _optimal_ value function $V^*$ (and thus an optimal policy), we replace the expectation over $\pi$ with a maximization over actions:
$$V^(s) = \max_{a\in\mathcal A}\Bigl[R(s,a) + \gamma \sum_{s{\prime}}P(s{\prime}\mid s,a)\,V^(s{\prime})\Bigr].$$
Likewise,
$$Q^(s,a) = R(s,a) + \gamma \sum_{s{\prime}}P(s{\prime}\mid s,a)\,\max_{a{\prime}}Q^(s{\prime},a{\prime}).$$

> **Interpretation:** This set of nonlinear equations characterizes the unique fixed point $V^*$, and underlies algorithms like Value Iteration and Q-Learning.

---

## **5. Derivation Sketch**

1. **Start** from the definition of $V^{\pi}(s)$.
2. **Expand** the return sum one step:$$V^{\pi}(s) = \mathbb{E}[R_{1} + \gamma\,R_{2} + \gamma^{2}R_{3} + \cdots] = \mathbb{E}[R_{1} + \gamma\,V^{\pi}(S_{1})]$$
3. **Condition** on the first action $A_{0}=a$ and first successor $S_{1}=s{\prime}$, then average under $\pi$ and $P$.
4. **For optimality**, replace the expectation over \pi with \max_{a}.

---

## **6. Why It Matters**

- **Dynamic Programming:** Policy iteration alternates between evaluating $V^{\pi}$ via the Bellman expectation equation and improving $\pi$ via a greedy step on $Q^{\pi}$.
- **Convergence Guarantees:** For finite MDPs with $\gamma<1$, repeated application of the Bellman optimality update converges to $V^*$.
- **Model-Free RL:** Even without known $P,R$, one can sample transitions and use temporal-difference methods (e.g., $TD(0)$, $Q$-Learning) to approximate the Bellman updates.
    

---

## **7. Simple Example**

Consider a two-state MDP $\{s_1,s_2\}$, single action with
$$P(s_2\mid s_1)=1,\quad R(s_1)=0,\quad P(s_1\mid s_2)=1,\quad R(s_2)=1,\quad \gamma=0.9.$$

The Bellman optimality equations are:
$$

\begin{cases}

V^(s_1) = 0 + 0.9\,V^(s_2),\\

V^(s_2) = 1 + 0.9\,V^(s_1).

\end{cases}

$$
Solving yields:

$$V^{s_1}=\frac{0.9}{1-0.9^2}\approx4.737,\quad V^{s_2}=\frac{1}{1-0.9^2}\approx5.263.$$

---

### **Key Takeaways**

- **Bellman equations** decompose the global, infinite-horizon value into local, one-step rewards plus discounted future values.
- They form the backbone of both **exact** (dynamic programming) and **approximate** (reinforcement learning) solution methods.
- Understanding their structure is crucial for algorithm design, convergence analysis, and extending to function approximation.
