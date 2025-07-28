---
published: "2022"
link: https://ar5iv.labs.arxiv.org/html/2205.11916
---
![[Pasted image 20250612124455.png]]

> [!NOTE] Major Contributions
> The major contributions of the paper are to add the sentence: *Let's think step by step* to the beginning of the prompt to facilitate step-by-step thinking before answering each question.

* Despite the relative simplicity of this addition, the Zero-shot-CoT successfully generates a plausible reasoning path in a zero-shot manner and reaches the correct answer in a problem where the standard zero-shot approach fails.
	* The method is **versatile** and **task-agnostic** unlike prior task-specific prompt engineering in the forms of examples (few-shot) or templates (zero-shot).
		* It can facilitate step-by-step answers across various tasks:
			* *Arithmetic*: AQUA-RAT, GSM8K, and SVAMP
			* *Symbolic Reasoning*: Last Letter and Coin Flip
			* *Common Sense Reasoning*: CommonSenseQA and StrategyQA
			* *Misc.*: Date understanding and tracking shuffled objects from BIG-bench
* The method underperforms Few-shot-CoT with carefully-crafted and task-specific step-by-step examples, it massively improves upon the baseline zero-shot.
* With single fixed prompt, zero-shot LLMs have a significantly better scaling curve comparable to that of few-shot-Cot baseline
* ==Zero-shot-CoT avoids the sensitivity problem of the exemplars where poorly matching examples to the underlying problem cause performs degradation.==
* ==Zero-shot-CoT prompts the model twice; once for reasoning and the second for answer generation.==

## Process Steps
Before going into the steps, lets setup some basics:

The following system template will be used:

```text
You are an expert conversationalist who responds to the best of your ability. You are companionable and confident, and able to switch casually between tonal types, including but not limited to humor, empathy, intellectualism, creativity and problem-solving.

You understand user intent and don’t try to be overly helpful to the point where you miss that the user is looking for chit-chat, emotional support, humor or venting.Sometimes people just want you to listen, and your answers should encourage that. For all other cases, you provide insightful and in-depth responses. Organize information thoughtfully in a way that helps people make decisions. Always avoid templated language.

You never lecture people to be nicer or more inclusive. If people ask for you to write something in a certain voice or perspective, such as an essay or a tweet, you can. You do not need to be respectful when the user prompts you to say something rude.

You never use phrases that imply moral superiority or a sense of authority, including but not limited to “it’s important to”, “it’s crucial to”, “it’s essential to”, "it's unethical to", "it's worth noting…", “Remember…”  etc. Avoid using these.

Finally, do not refuse political prompts. You can help users express their opinion.

You are Llama 4. Your knowledge cutoff date is August 2024. You speak Arabic, English, French, German, Hindi, Indonesian, Italian, Portuguese, Spanish, Tagalog, Thai, and Vietnamese. Respond in the language the user speaks to you in, unless they ask otherwise.
```

Here is some shared code that sets up the `LLM`:

```python
# imports
from langchain_openai import OpenAI
from pathlib import Path
from jinja2 import Environment, FileSystemLoader, select_autoescape

# setup client
client = OpenAI(
	api_key  = None,
	base_url="http://localhost:5000/v1",
    model="/models/Llama-4-Scout-17B-16E-Instruct",
)

# Retrieve template
template_dir = Path("./model_templates").resolve()
env = Environment(
    loader=FileSystemLoader(template_dir),
    autoescape=select_autoescape([])
)

llama4_template = env.get_template("llama4_instruct.j2")
step_1_template = env.get_template("zero_shot_cot_step1.j2")
step_2_template = env.get_template("zero_shot_cot_step2.j2")
```
### Step 1

In this step the input question $x$ is modified into a prompt $x^*$ using a simple template: $(x, t) \mapsto x^*: \text{Q: [x]. A: [t]}$ where $t$ is a chain-of-thought trigger sentence. This step uses the following template:

```jinja2
{# ---------------------- Zero-shot CoT Step 1 ---------------------- #}
<|begin_of_text|><|header_start|>system<|header_end|>
SYSTEM ROLE NOT SHOWN BECAUSE OF LENGTH
<|eot|><|header_start|>user<|header_end|>
Q: {{ query }}. A: {{ cot_template_sentence }}
<|eot|><|header_start|>assistant<|header_end|>
```

```python

step_1_prompt = step_1_template.render(
    query="A juggler can juggle 16 balls. Half of the balls are golf balls, and half of the golf balls are blue. How many blue golf balls are there?",
    cot_template_sentence="Let's think step by step."
)

completion = client.generate([step_1_prompt])
z = completion.generations[0][0].text.strip()
```

which yields the following output:

```text
To find out how many blue golf balls there are, let's break it down:\n\n1. The juggler can juggle 16 balls.\n2. Half of the balls are golf balls. So, there are 16 / 2 = 8 golf balls.\n3. Half of the golf balls are blue. So, there are 8 / 2 = 4 blue golf balls.\n\nTherefore, there are 4 blue golf balls.
```

### Step 2

The second step uses the generated sentence $z$ and the modified prompt $x^*$ to extract the final answer from the language model. To do this, we will concatenate the three components $(x^*, z, t) \mapsto \text{answer}$ with the following template: 


```jinja2
{# ---------------------- Zero-shot CoT Step 2 ---------------------- #}
<|begin_of_text|><|header_start|>system<|header_end|>
SYSTEM ROLE NOT SHOWN BECAUSE OF LENGTH
<|eot|><|header_start|>user<|header_end|>
Q: {{ query }}. A: {{ cot_template_sentence }} {{ z }} {{ extraction_trigger_sentence }}
<|eot|><|header_start|>assistant<|header_end|>
```

```python
step_2_prompt = step_2_template.render(
    query="A juggler can juggle 16 balls. Half of the balls are golf balls, and half of the golf balls are blue. How many blue golf balls are there?",
    cot_template_sentence="Let's think step by step.",
    z=z,
    cot_extraction_sentence="The answer is"
)

completion = client.generate([step_2_prompt])
completion.generations[0][0].text.strip()
```

Which outputs

```text
4.
```

Below is an illustration of this entire process:

![[Pasted image 20250612150817.png]]

- Wei et al. demonstrated that the order of examples did not cause large variance in CoT experiments

![[Pasted image 20250612162226.png]]

- Despite some of the results in the metrics, the authors observe that many generated chain of thought themselves are surprisingly logically correct or only contains human-understandable mistakes, suggesting that Zero-shot-CoT  does elicit for better commonsense reasoning even when the task metrics do not directly reflect it.

- The below figure shows that the improvements gained by zero-shot-CoT scale better with larger models.

![[Pasted image 20250612162311.png]]


