# Attendees
- Eddy
	- Lawrence Livermore
	- Project CRC and Archer team head
		- Software assurance portfolio
		- Working with Air Force and Program Offices directly
- John Breneman
	- Lawrence Livermore
	- Seems like a lead of some type over the others
- Leo
	- Lawrence Livermore
	- Key researcher behind *Code2Doc*
	- CS degree - Center for Applied Scientific Computing
	- Research into LLMs and how they can help in c
- (Someone that I couldn't hear) (might be Eddy)
	- Started Rose project over 30 years ago
- Andre Leone
	- SD Execution Lead for ABMS
	- Heads AIML consortium
- Geoffrey Dolinger
	- Director of Academic Research (SWORD)
- Robert "Bob" Cane
	- Technical program manager for the CRC (deployable system branch)
- AJ Nefcy
	- Works with Bob Cane
	- Make a CICD pipeline and acquire a variety of tools that they hook up to that
- Lee Shuman
	- Works in assurance and software development and supports the ABMS teams
- Zackery Herman
	- Works under Thundercamp  (PAAS for DevSecOps)
	- Pathfinding LLM efforts

# Presentation Notes
- Advisement for the Air Force at Large for acquisition and sustainment of AIML as well as the use cases of LLMs
- **Code2Doc**
	- *Presenter* - Chunhua "Leo" Liao
	- Ollama
	- Quantization
	- A Pipeline using Doxygen and LLMs
		- Locally Deployed
		- ![[Pasted image 20250721121745.png]]
			- Assess quality of existing comments (extract comments phase -> Eval)
			- If no comment we can prompt the LLMs to generate comments
		- **Evaluation**
			- Functionality
			- Input Parameters
			- Side Effects: Mention side effects
			- Return Value
			- Error Handling
			- Consistency: Alignment of comments with actual function behavior
			- Edge Cases
			- Sufficient Length

# Questions
1. For quality of comments you are using zero-shot prompting. Have you guys tried  train-of-thought or something similar to pull in API docs from external sources? How does the model handle version changes for libraries, etc. 