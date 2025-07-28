---
tags:
  - "#work"
  - "#gap-analysis"
---

# Misc. Talk 1

```mermaid
flowchart TD
	subgraph DI["Document Ingestion"]
	    PWS["Performance Work Statement"]
	    CDRL[CDRLs]
	    TD["Technical Documents"]
	end

	A["Chunk Requirements Into Sections"]
	
	subgraph CleanDocs["Clean & Chunk"]
		B["Clean Documents"]
		Endpoint["Hit Endpoint To Expand Acronyms"]
		StoreChunks["Store Chunks In Vector DB"]
	end

	B --> Endpoint
	B --> StoreChunks

	D["Develop A List Of Questions Per Subsection"]
	E["Query Chunks Per Question"]

	

	PWS --> A
	CDRL --> CleanDocs
	TD --> CleanDocs

	subgraph AnswerGeneration["Generate Question/Answer Pair"]
		F["LLM Generated Answer"]
		G["Confirm Answer With Separate LLM Persona"]
		H["Request Addtional Information From Human"]
		I{"Question Answered?"}
		NoAnswer["Question Not Answered List"]
		Answer["Question Answered List"]
		PartialAnswer["Question Partially Answered List"]
	end
	
	A --> D
	D --> E

	E --> AnswerGeneration
	F --> G
	F -->|"Needs Additional Information"| H
	H --> F
	G --> I
	I --> |no| NoAnswer
	I --> |yes| Answer
	I --> |partial| PartialAnswer
	
```










## Key Points

- Have an endpoint where an acronym can be sent and the expansion returned `/get`
- Chunk the *PWS* into different sections ($X.X.X$ sections)
	- Develop a list of questions per section
	- First point of human intervention would be allowing the engineers to refine/enhance the requirement descriptions before generating the questions.
	- Second point of human intervention is grooming the list of questions made by the LLM
	- 

## Questions:

- Can we export PowerPoint documents as HTML5?
- 





