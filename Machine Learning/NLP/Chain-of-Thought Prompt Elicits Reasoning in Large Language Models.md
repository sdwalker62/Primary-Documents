---
published: Jan 10, 2023
link: https://ar5iv.labs.arxiv.org/html/2201.11903
---
![[Pasted image 20250612094147.png]]

Above is an example of a small change to the prompt that allowed PaLM to solve a math challenge without the need for retraining.

- Scaling up the model size has shown to confer a range of benefits such as sample efficiency and improved performance [^1]
	- Improved performance could mean that larger models have emergent abilities
	- **Look into the sample efficiency paper!**
- Scaling up model size alone has not proved sufficient for achieving high performance on challenging tasks such as math, commonsense, and symbolic reasoning.
- Math reasoning can be aided by generating natural language rationales that lead to the final answer.
	- Work in 2017 by Ling et. al has granted the model the ability to generate natural language intermediate steps by training from scratch or finetuning a pretrained model, in addition to neuro-symbolic methods that use formal languages instead of natural language.
	- ==A key limitation of this is the associated cost of creating a large set of high quality rationales, which is much more complicated than simple input-output pairs used in normal machine learning==
- LLMs offer the prospect of in-context few-shot learning via prompting. Instead of finetuning a separate language model checkpoint for each new task, you can simply "prompt" the model with a few input-output exemplars demonstrating the task. 
	- ==This works poorly on tasks that require reasoning abilities , and often does not improve substantially with increasing language model scale==
- This paper proposes that it can combine the strengthens to the above ideas without their pitfalls.
	- They explore the ability of the LLM to perform few-shot prompting for reasoning tasks, given a prompt that consists of triples: `<input, chain_of_thought, output>`. A chain of thought is a series of intermediate natural language reasoning steps that lead to the final output.
- *Chain-of-thought prompting has several attractive properties as an approach for facilitating reasoning in language models.*
	1. First, chain of thought, in principle, allows models to decompose multi-step problems into intermediate steps, which means that additional computation can be allocated to problems that require more reasoning steps.
	2. Second, a chain of thought provides an interpretable window into the behavior of the model, suggesting how it might have arrived at a particular answer and providing opportunities to debug where the reasoning path went wrong (although fully characterizing a model’s computations that support an answer remains an open question).
	3. Third, chain-of-thought reasoning can be used for tasks such as math word problems, commonsense reasoning, and symbolic manipulation, and is potentially applicable (at least in principle) to any task that humans can solve via language.
	4. Finally, chain-of-thought reasoning can be readily elicited in sufficiently large off-the-shelf language models simply by including examples of chain of thought sequences into the exemplars of few-shot prompting.
* ==Chain of thought reasoning is an emergent ability of model scale, therefore it does not positively impact performance for small models ($<100$ billion parameters)==
* ==Chain of thought prompting has larger performance gains for more-complicated problems.==
* ==It is likely that chain of thought prompting does not depend on a particular linguistic style. ==
	* The authors had different people construct the prompt exemplars and all of the results were still above the baseline.
	* It also seems that the method is robust to the number of exemplars as well.
	* ![[Pasted image 20250612100400.png]]
* ==The language-based nature of chain of thought actually makes it applicable to a broad class of commonsense reasoning problems, which involve reasoning about physical and human interactions under the presumption of general background knowledge.==
	* ![[Pasted image 20250612100548.png]]
* 

[^1]: More information would be nice. What does "improved performance" mean?
