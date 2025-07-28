# Definition of ML

 > What is Machine Learning? 

Broader notion of building computational artifacts that learn over time based on experience. 

## Supervised Learning

In short, supervised learning is ==function approximation==. Taking labeled datasets and computing a function that maps inputs to labels. Our objective is to compute an approximate function that accurately labels as many data points as possible. The function which maps all data points to their correct label is the _true function_. 

The fundamental problem in Machine Learning is generalization. We normally will only have a small labeled subset of all possible data, we must train a model on this small subset which can effectively generalize too unseen data. This is known as _extrapolation_.

Supervised learning is about _induction_, as opposed to _deduction_. Induction is the process of going from a handful of examples to a more general rule. Deduction on the other hand, is the process of going from a general rule to specific instances. In the beginning, AI was mostly about deductive reasoning. With deduction, we can deduce that certain things hold given information, for instance if we know that $A \Rightarrow B$  and I tell you that $A$ has been observed, then we can infer $B$. With induction we seek patterns, if you know the sun rose on Monday, Tuesday, Wednesday, and Thursday, then we can infer that it is likely to rise on Friday. Unlike $A \Rightarrow B$, we do not have a rule which tell us this such as $\text{Friday} \Rightarrow \text{sun}$, but we can infer from the pattern that such an event is likely.

#### Inductive Bias

In supervised learning we have _inductive bias_. Inductive bias is when you restrict your hypothesis space to a certain class of hypotheses. In simple terms, it is a guess about what the true function looks like, before analyzing the data. An elementary example would be regression. If you have a finite set of examples, then you can fit an infinite number of functions to them. If you assume that the true function is linear, then you limit your search to the set of all possible linear functions. This narrows the hypothesis space, and makes searching for an approximate function feasible. Without this restriction, it would impossible to perform Machine Learning, since we would have too many hypothesis to search through. Certain data leads to inductive bias, such as CNNs with image data. 

A consequence of this is the _No Free Lunch Theorem_, which states that if your inductive bias works well on some types of data, it has to work poorly on other types of data. There is no model that solves every problem!

## Unsupervised Learning

In unsupervised learning, we have some examples and seek to derive some structure by analyzing the relationships between the inputs themselves. A simple example would be grouping animals into families as a kid. You take examples of animals and analyze their properties, taking animals with common properties and labeling them together. For instance animals with wings would be labeled as birds, etc. Unsupervised learning is about ==description==. It is about taking a set of data and figuring out how you might partition in one way or another. 

This is different than supervised learning. The partitions that we form using unsupervised learning are all equally valid absent a signal which ranks one above the other. In supervised learning, there is an absolute signal which provides details on how the examples should be partitioned. 

## Reinforcement Learning

In Reinforcement Learning, we gather experience via an _agent_ interacting with an _environment_. The agent can interact with the environment via _actions_, and the environment responds to the agent via _observations_ and _rewards_. The rewards the agent receives act as our feedback signal, which informs the agent on which actions in which states were good and which were bad. 

Unlike with the other forms of learning, our feedback may be delayed. The agent may progress through the environment and receive feedback based on events that happened a few steps in the past. For instance, if the agent is playing tic-tac-toe, the agent may win or lose a game at time step $t$. The finishing move and reward occurred at time step $t$, but at the previous time steps the agent's actions setup the termination state of the game. The challenge then is to understand what series of events lead to this outcome and train the agent to maximize future rewards and not just immediate rewards. It is similar to playing a game and not knowing the rules, just receiving positive or negative feedback when taking actions based on your current observations. 

## Optimization

In some sense, the three forms of Machine Learning can be framed as optimization problems. In supervised learning, we seek to label the data well by approximating the true function well. In unsupervised learning we seek to define a criterion that partitions the data such that the resulting cluster scores well. And in reinforcement learning, we seek to find a policy that causes the agent to behave well by measure of expected long term reward. 

## Data

For all forms of Machine Learning, ==data is king==. In Computer Science, algorithms are central, whereas in Machine Learning, data is central. 