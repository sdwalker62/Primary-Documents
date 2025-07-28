---
tags:
  - cs7641
  - omscs
  - optimization
  - machine-learning
ed link: https://edstem.org/us/courses/71185/lessons/126665/slides/706895
---

## Optimization Problem Statement

> Given an input space $X$ and an objective (fitness function) $f:X \rightarrow \mathbb{R}$ we are are searching for the optimal $x^* \in X$ such that we maximize the value of $f$, or $f(x^*) = \max_x f(x)$. 

* This might not be the global optimum, but approximately close enough, i.e. if $x^*$ is optimal and $x^{**}$ is our solution, then we want $\| x^{**} - x^* \| < \delta$ for some sufficiently small value of $\delta$.
* **Example 1:** For a chemical plant the variables to your function could be chemical quantities and the function maximizes product yield. We want to find the amounts of each chemical that can produce the best yield.
* **Example 2:** The weights are parameters of a neural network, so we could optimize these parameters such that we minimize the error. 
* If your input space is small and enumerable you could enumerate all possible values and determine the optimal value $x^*$. 
	* This works particularly well if you have a complex function
* If you are in a continuous space, analytical ways could work (i.e. finding the derivative and finding the values that of $x^*$ where the graph crosses the $y$ axis; you could also use Newton's method)
	* If you are going the derivative route, the function must have a derivative (functions like module don't for certain values of $x$)
	* Newton's method also requires a derivative and can stuck in a local optimum. (derivatives can too, but if you can analytically solve for the derivative, i.e. you have the true function, then you can check each parameter combination where $D_xf =0$)

The above begs the question, what happens if you have a large input space and therefore cannot use enumeration and cannot find the derivative (or it is hard to find) and the function potentially has many local optima? That is where **randomized optimization** can help.

## Hill Climbing

More information can be found in the [[Hill Climbing]] note.

> First we guess a value $x \in X$ to set as our initial input value. Then in a neighborhood $N$ around $x$, we check to see if we can find values that improve $f$. We can do this by looking at each neighbor of $x$ (as determined by some step size in the chosen direction) and evaluating the function $f$ at that point. If the function evaluated at that point is larger, then we will set that input to be our new argmax and repeat this process until we cannot find a value that improves the function.

**Advantages:**
1. Simple to implement.
2. Cheap to compute for most functions.

**Disadvantages:**
1. Will likely get stuck in a local optima.

### Randomized Restart Hill Climbing

With randomized restarts, the hill climbing algorithm has a greater likelihood of not getting stuck in a local optima. The idea is to restart once a optima has been obtained from normal hill climbing. We can record each optima found and select the largest one, which is hopefully the global optima. 

**Advantages:**
1. Multiple retries increases the likelihood of achieving a good result.
2. Not much more expensive than the normal version. The cost increase is constant multiple of the number of retries. 
3. Greater coverage of the input space (although not guaranteed).

## Simulated Annealing

More information can be found in the [[Machine Learning/Optimization/Simulated Annealing]] note.

Don't always improve - sometimes you need to search (explore). Blacksmiths figured out that one method of strengthening a blade is to repeatedly heat and cool it so that the molecules can move into a configuration that has lower potential energy. We can borrow this idea of repeated heating and cooling for finding a optima. 

> *For a finite set of iterations*:
> 1. Sample a new point $x_t \in N(x)$ 
> 2. Jump to a new sample with probability given by an acceptance probability function $P(x, x_t, T)$ 
> 		$$P(x, x_t, T) = \begin{cases} 
       1, & f(x_t) \geq f(x) \\
       \exp\left(\frac{f(x_t) - f(x)}{T}\right), & \text{otherwise} 
 \end{cases}$$
> 1. Decrease temperature $T$

### Some Notes
1. Large values of $T$ means we are more likely to accept the new point, regardless of the difference (very random).
2. Low values of $T$ means any difference blows up and we only move uphill (the top case). Essentially this reduces us to hill climbing.
3. $T$ should be strictly larger than zero

### Properties

1. $T \rightarrow \infty$ we get random walk
2. $T \rightarrow 0$ we get hill climbing
3. We want to decrease $T$ slowly
	1. Large values of $T$ means that small valleys are no longer barriers and only the largest valleys are barriers
	2. As we decrease the values of $T$ then we are stopped by smaller and smaller valleys
	3. The theory is that if we start with large values of $T$, we quickly move to the region where the optima is located and as we decrease the value of $T$ we refine our search to more local regions of the parameter space. 

## Genetic Algorithms

More information can be found in the [[Machine Learning/Optimization/Genetic Algorithms]] note.

A genetic algorithm takes some initial population and selects the most fit, then we least fit and replace them with mutations of the most fit. By doing this we hope to eventually find a member of the population that is optimal. 

> Start with an initial population $P_0$ of size $k$.
> Repeat until converged:
> 1. Compute the fitness score of all members of $P_0$ 
> 2. Select the most fit (top half - truncation selection, weighted probability - roulette wheel)
> 3. Pair up the members, replacing the least fit members via crossover or mutation

## MIMIC

More information can be found in the [[MIMIC]] note.

Born from the observation that with the above algorithms, you transition between points, but don't learn any structure of the loss space along with way. With the randomization, it was also unclear what probability distribution we are dealing with. Charles Isbell wrote the paper on MIMIC. 

The main idea of MIMIC is to directly model the probability distribution. This distribution will be refined over time as we learn more about the structure of the parameter space. 

$$
\Pr\{\theta; x\}= \begin{cases} 
       \frac{1}{z_\theta}, & f(x) \geq \theta \\
       0, & \text{otherwise} 
 \end{cases}
 $$
We can think of this like slicing a mountain and only sampling from values in the half.

1. $\Pr\{\theta_\max, x\}$ is a uniform distribution over the optima
	1. $\theta_\max$ is the largest value that $f$ can return which is the optimum of the function
	2. The probability distribution will assign a value of 1 to the optimum if there is a single optimum and a uniform distribution over them if there are multiple
		1. If there are 4 optimum points then we would have a probability of 1/4 for each
2. $\Pr\{\theta_\min, x\}$ is a uniform distribution 
	1. $\theta_\min$ is the smallest value that the $f$ can achieve, therefore all other points are greater than or equal.
	2. Thus, the probability distribution is a uniform distribution over all of the points in the input space.

### High Level Pseudocode

> 1. Generate samples from $\Pr\{\theta_t; x\}$ 
> 	1. Set $\theta_{t+1}$ to the $n^{th}$ percentile 
> 	2. Retain only those samples such that $f(x) \geq \theta_{t+1}$
> 	3. Estimate $\Pr\{\theta_{t+1}; x\}$ 
> 	4. Repeat

We hope to move from $\theta_\min \rightarrow \theta_\max$ as the algorithm progresses.

### Estimating Probability Distributions

Let's start with the chain rule representation of a probability distribution:

$$\Pr\{x\}=\Pr\{x_1\mid x_2, x_3, \ldots x_n\}\Pr\{x_2 \mid x_3, x_4, \ldots x_n\}\cdots \Pr\{x_n\}$$

where $x=(x_1, x_2, \ldots , x_n)$. We could estimate this joint distribution, but that would be difficult. We can make some assumptions about conditional independence to make this problem easier. Specifically, we can make the assumption that we only care about dependency trees.

### Dependency Trees

A dependency tree is a special case of a Bayesian network where the network itself if a tree. That is, every node and every variable in the tree has exactly one parent. They are a directed acyclic graph. This means that every node (variable) depends only on one other variable, which simplifies our above joint distribution significantly. If $\pi$ means parent, then 

$$\hat{\Pr}\{\pi; x\}= \prod \Pr\{x_i;\pi(x_i)\}$$
When comparing this representation with the original a few nice properties emerge:
1. You are only every conditioning on *at most* one other variable (for instance the start of the tree has no dependency so it conditions on zero other variables). Thus $\pi$ would return itself, $\pi(x_0)=x_0$. (They mention that is Naive Bayes every node has the same parent). If everyone had no parents, then the variables are independent of one another.
2. Since the variables have at most a single parent the conditional probability tables are small.
	1. The tables are linear in the number of features.
	2. In order to get the tree we will need to keep track of a quadratic set of variables (not sure what this means yet).
3. Dependency trees allow you to represent relationships between features. Since dependency trees only allow you to keep track of a single dependency for each variable, they are the simplest set of relationships we could keep track. The next simplest would be the case where each feature is independent of one another. The most complex is where all features are related.

**Note** that MIMIC does not require a dependency tree, we use them here because you have to make some decision about how to represent probability distributions and this is the easiest thing we can do and still capture relationships. At the very least this will allow us to capture the same kinds of relationships that we get from crossover in genetic algorithms (which served as the inspiration for this method). Crossover does represent structure, in this case structure that is measured by locality and dependency trees are a general form of that. Dependency trees are better because it does not require locality the way crossover does. 

Dependency trees are also very easy to sample from. 

We do not know the true probability distribution so we need to estimate it. To find an approximate distribution, we need a measure of how close our approximate distribution is to our true distribution. For this, we can use the Kullback-Liebler divergence:

$$
\begin{aligned}
D_\text{KL}(p\mid\mid \hat{p}_\pi) &= \sum_i p\log\left(\frac{p}{\hat{p}_\pi}\right) \\
&=-h(p) + \sum_i h(x_i \mid \pi(x_i)) \\
J\pi&=\sum_i h(x_i \mid \pi(x_i))
\end{aligned}
$$
In other words, the distribution (the best tree that we can find) that minimizes the KL divergence is the one that minimizes entropy $h$ for each of the features $x_i$ given its' parent $\pi(x_i)$. 

It turns out that computing the above equation in its current form is difficult, therefore we will compute an alternate form that will still minimize the divergence, $\min D_{KL}$.

We can add a term, $h(x_i)$ that does not depend on our choice of $\pi$ and therefore does not change the minimization problem. We will call this new form $J'_\pi$,

$$
J'_\pi = -\sum_i h(x_i) + \sum_i h(x_i \mid \pi(x_i))
$$
By adding this term we get the negative of mutual information. 

$$
\min J'_\pi = -\min\sum_i I(x_i; \pi(x_i))
$$
or the dual problem

$$
\max J'_\pi = \max\sum_i I(x_i; \pi(x_i))
$$
The reason this is helpful is because it provides us with a relatively simple algorithm for finding a dependency tree. The trick here is to realize that conditional dependencies are directional, whereas mutual information is bi-directional. To find the best dependency tree you should maximize the mutual information between a variable and its parent. This make sense since a variable wants to be associated with a parent that gives the most information about itself. 

This dependency structure is a [[Fully Connected Graph]]. The optimal dependency tree is a [[Maximal Spanning Tree]]. Since this is a densely connected graph, [[Prim's Algorithm]]
is the proper search strategy to use to find the tree. 

### Practical Matters

* MIMIC does well with structure
	* This is in comparison to other optimization algorithms such hill climbing which can get confused because two optima could be identical but look very different from one another. These other algorithms get torn in different directions since they only look at the point values. 
* Representing $p^\theta, \hspace{1em} \forall \theta$ 
	* It is not enough to just represent a probability distribution of the optima, we also need to represent everything else in-between as you move through probability space toward your answer. 
* Local optima are still a problem
* There is a wealth of probability theory that could be leveraged when using MIMIC
* What is the practical time complexity of using MIMIC?
	* MIMIC tends to run orders of magnitude fewer iterations than other algorithms (claims Charles Isbell)
	* For instance, Simulated Annealing might take 100,000 iterations to find an answer, whereas MIMIC can find it much faster at only 100. ==Although this does not take into account how long each iteration takes to run==.
	* The upside is that MIMIC gives you more information about your parameter space since you get structure
	* MIMIC tends to work very well when the cost of evaluating the fitness function is high
		* Examples of this are things like simulations that can be costly or if you need a human evaluator 



$$
\begin{aligned}
\mathcal{L}(\theta) &= \mathbb{E}_{\mathbf{x} \sim p_{\text{data}}(\mathbf{x})} \left[ \log p_\theta(\mathbf{x}) \right] - \frac{1}{2} \sum_{i=1}^n \frac{(\mu_i - \hat{\mu}_i)^2}{\sigma_i^2 + \epsilon} \\
&\quad + \int_{\mathbb{R}^d} \left( \nabla_\theta \log q_\theta(\mathbf{z}) \right)^T H(\theta)^{-1} \left( \nabla_\theta \log q_\theta(\mathbf{z}) \right) q_\theta(\mathbf{z}) \, d\mathbf{z} \\
&\quad + \det\left( 
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
\right)
\end{aligned}
$$

