
# Bayesian Learning

* Each observed training example can incrementally decrease or increase the estimated probability that a hypothesis is correct. This provides a more flexible approach to learning than algorithms that completely eliminate a hypothesis if it is found to be inconsistent with any single example.
* Prior knowledge can be combined with observed data to determine the final probability of a hypothesis. In Bayesian learning, prior knowledge is provided by asserting (1) a prior probability for each candidate hypothesis $p(h)$, and (2) a probability distribution over observed data for each possible hypothesis $p(D \mid h)$. 
* Bayesian methods can accommodate hypothesis that make probabilistic predictions (e.g. hypotheses such as "this pneumonia patient has a 93% chance of complete recovery").
* New instances can be classified by combining the predictions of multiple hypotheses, weighted by their probabilities.
* Even in cases where Bayesian methods prove computationally intractable, they can provide a standard of optimal decision making against which other practical methods can be measured.
* One difficulty about Bayesian learning is that they typically require initial knowledge of many probabilities. Another is the significant computational cost required to determine the Bayes optimal hypothesis in the general case. 

## Bayes Theorem

Bayes theorem provides a mechanism to compute the most probable hypothesis in $H$ given the observed training data $D$. Some notation:
* $P(h)$ is the initial probability that hypothesis $h$ is true, before observing the training data and is called the *prior probability* of $h$ and may reflect any background knowledge we have about the likelihood of $h$ is correct. If no background knowledge is available, then we may select $P(h) \sim \text{Uniform}(H)$.
* $P(D)$ is the prior probability that training data $D$ will be observed. This is independent of which hypothesis is true and is a property of the data itself.
* $P(D\mid h)$ denotes the probability of observing data $D$ given some world in which hypothesis $h$ is true.
* $P(h \mid D)$ is the probability of hypothesis $h$ given we have observed data $D$. $P(h \mid D)$ is the *posterior probability* of $h$ because it reflects our confidence that $h$ is true after observing the training data $D$. 
We can relate these quantities via Bayes theorem:
$$P(h \mid D) = \frac{P(D \mid h)P(h)}{P(D)}$$
The likelihood of a hypothesis given some training data $D$ increases with the probability of observing that data given that hypothesis is true and the prior probability over $h$, or $P(h \mid D) \propto P(D \mid h)P(h)$. The likelihood decreases in proportion to the likelihood of $D$. If the probability of observing the training data $D$ is highly probable, then the evidence for a particular hypothesis $h$ given that $D$ is weaker. 

Often we want to find the most probable hypothesis, $h \in H$, given training data $D$. We will denote this optimal hypothesis $h_{MAP}$ for *maximum a posteriori*. 

$$
\begin{split}
h_{map} &= \arg\max_{h \in H} P(h \mid D) \\
&= \arg\max_{h \in H} \frac{P(D \mid h)P(h)}{P(D)} \\
&\propto \arg\max_{h \in H} P(D \mid h)P(h)
\end{split}
$$
In some cases, we will assume that every $h \in H$ is equally likely a priori ($P(h_i) = P(h_j), \, \forall h_i, h_j \in H$). This further reduces the expression to only depend on $P(D \mid h)$. $P(D \mid h)$ is called a *maximum likelihood* (ML) hypothesis, $h_{ML}$. 
$$ h_{ML} = \arg\max_{h \in H} P(D \mid h)$$
## Brute-Force Bayes Concept Learning

Assume a learner considers some finite hypothesis space $H$ defined over the instance space $X$, in which the task is to learn some concept $c:H \rightarrow \{0, 1\}$. Assume the learner is provided some sequence of training examples $\left< <x_1, d_1>, \ldots, <x_m, d_m> \right>$ where $x_i \in X$ and $d_i = c(x_i)$. Also assume that the sequence of instances $\left< x_1, \ldots, x_m \right>$ is static and the training data $D$ can be written $D=\left< d_1, \ldots, d_m \right>$. We can design an algorithm that outputs $h_{MAP}$ using Bayes theorem:

1. For each hypothesis $h \in H$, calculate the posterior probability $$P(h \mid D) = \frac{P(D \mid h)P(h)}{P(D)}$$
2. Output the hypothesis $h_{MAP}$ with the highest posterior probability $$h_{MAP} = \arg \max_{h \in H} P(h \mid D)$$
This algorithm will be computationally expensive due to the need to compute $P(h \mid D)$ for all $h \in H$, but it is still of interest since it provided a standard against which we may judge the performance of other concept learning algorithms. 

## MAP Hypotheses and Consistent Learners

We will say that a learning algorithm is a *consistent learner* provided it outputs a hypothesis that commits zero errors over the training examples. Every consistent learner outputs a MAP hypothesis, if we assume $P(h) \sim \text{Uniform}(H)$ and we assume deterministic, noise-free training data $\mathbb{1}$ 

Can you succinctly describe the strengths and weaknesses of Value Iteration to a graduate student. Return your response in the form of a table in Markdown format.
