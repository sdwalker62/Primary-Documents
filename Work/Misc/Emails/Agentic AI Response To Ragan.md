---
created: 2024-07-15
tags:
  - "#work"
  - "#email"
---
The 577th AIML team is exploring the use of Agentic AI in the Gap analysis solution for the OPIR satellites. The Gap analysis presents a low-stakes environment for exploring graph-based Agentic AI in a narrow scope that will enable rapid prototyping with available human feedback. We hope to transfer any lessons learned in this domain to both NITMRE and EOD as well as any future NLP-based AIML requirements. Currently on SERN we have a Llama 4 model hosted that has been endowed with the ability to call certain tools that we consider 'safe', meaning tools like output formatters, calculators, and web scrapers. The model does not have the ability to execute arbitrary code or produce artifacts and transmit them without human supervision. 

We currently employ a mixture of LangGraph and LangChain for the backbone of the Agentic AI codebase and use what is known as Graph-of-Thought as a method for planning execution pathways. The LLM can transverse the planned nodes as it searches for a satisfactory solution. This is the current state-of-the-art for open research and we hope to transfer this technology to NITMRE for their upcoming Emergent Situations v2 feature later this year. 