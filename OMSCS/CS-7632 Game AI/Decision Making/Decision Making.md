---
created: 2025-07-13
tags:
  - "#omscs"
  - "#computer-science"
  - "#game-ai"
link: https://gatech.instructure.com/courses/462870/pages/decision-making-overview?module_item_id=5021486
---
---
# Fuzzy Logic
[Lecture URL](https://mediaspace.gatech.edu/media/2021+Game+AI+-+Decision+Making+-+Fuzzy+Logic/1_or7bm9vq)

## Non-Numeric Linguistic Expression
Consider the scenario of making a grill cheese sandwich. You might have a recipe like the following:

1. Cut two slices of bread **medium thick.**
2. Turn the heat on the griddle on **high**.
3. Grill the slices on one side until **golden brown**.
4. Turn the slices over and add a **generous helping** of cheese.
5. Replace and grill until the top of the cheese is **slightly brown**.
6. Remove, sprinkle on a **small amount** of black pepper, and eat.

How could we automate this with a program that will decide what to do at each step. For instance, what is **golden brown**, it is not a discrete state but a gradient. Each step is:

- Subjective
- Vague
- Flexible Interpretation
- Challenge to coordinate with conventional logic
## Motivation

- *Fuzzy Logic*: truth degrees, vagueness, subjectivity
	- Consider: "20% chance of rain" vs "partly cloudy"
	- Probability as likelihood, ignorance, uncertainty
- *Linguistic*: non-numeric expression of rules & facts (e.g., new or old)
	- Allows for use of vague human assessments in computing problems
	- E.g. Cautious vs Confident
- *FSM w/ 2 states*: Switching looks unnatural
	- Cautious (range), sneak slowly (range)
	- Confident, walk normally
- *Value?*
	- Relatively popular in games industry
	- Largely dismissed in academic AI (because it is not based on observed probabilities or patterns)

## Fuzzy Logic

- Modeling of *imprecise concepts*
- Modeling of *imprecise dependencies*
- Superset of classical logic
- Introduces concept of [[Degree of Membership (DOM)]]
- Uses [[Fuzzy Sets]] and [[Fuzzy Rules]]
- **Not** probability

<figure style="text-align: center;">
  <img src="Pasted image 20250713150649.png" alt="Description" width="400">
  <figcaption style="font-style: italic">Figure 1: Temperature can be cold, warm, or hot. Instead of saying it is definitively one or the other we have degrees of membership for each set.</figcaption>
</figure>
Based on the membership in each set, we could define rules of behavior. For example, if the temperature is warm we might want to set the fan speed to a moderate setting. This would like something like

```
IF temperature IS very cold THEN fan_speed is stopped
IF temperature IS cold THEN fan_speed is slow
IF temperature IS warm THEN fan_speed is moderate
IF temperature IS hot THEN fan_speed is high
```

Note that this is a subjective measure since things like very cold and warm are not well-defined or universal. It might be reasonable to perform [[Linear Interpolation]] between two sets to determine membership.

## Fuzzy Logic Use Cases

- More direct way to represent expertise (linguistic form)
	- Potential for declarative authoring by non-programmers
- Opportunity to capture expertise (e.g., consult an expert) but lack the resources to train (Neural Network, etc.)
- Flexible behavior design paradigm
- When behavior design efficiency is more important than optimization
- Behaviors can act on multiple variables without imposing rigid structure to decision making

## Fuzzy Logic History

- Proposal of Fuzzy Set Theory Introduced in 1965 by Lotfi A. Zadeh (UC Berkeley)
- Japanese were the first to utilize for commercial applications in late 1970s-1980s (high-speed train, rick cookers, etc.)
- Use of Fuzzy Logic controllers really picked up in the late 1980s
- Research boom in the 1990s.




