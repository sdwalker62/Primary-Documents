
- T-shirt sizing for these

# Phase 1: Requirements Gathering / Refinement, Deciding Evaluation Metrics, and Feasibility Research

- KANBAN
- Try to limit to ~2 weeks (or sprint length)
	- S -> 2 weeks
	- M -> 4 weeks
	- L -> 8 weeks
- Gather requirements from the customer
	- Definition of Done
	- Proposed timelines
	- What is the hardware for each IL level
		- If we can get new hardware, what is the max?
- Determine metrics that will be used for the prototyping and feasibility phase
	- Acceptable and Preferred thresholds
	- Generic descriptions
	- Generic importance
- Can the customer provide data?
	- Yes: Do we need access to a system to get that data or a SME?
		- How long and where can this data live?
	- **No**: Can we get it ourselves?
	- If we can't get data we exit here
- **Deliverable Contents**
	- Research plan outline
	- How many FTE for phase 2?
- Figure out what metrics they need by asking questions and determining afterwards 
# Phase 2: Prototyping and Demo

- KANBAN
- Data Analysis (Phase 1 of 2)
- Security Research
- Periodic research briefs with SMEs
- **Deliverable Contents (Slide Deck)**
	- Security Analysis
		- COAs and Risks
	- Benchmarking (evaluations)
		- This could be done outside of the production software
			- Only caveat would be if performance (throughput) is the main metric
	- Timeline (roadmap) for phase 3 for each COA
	- Internal demo (solicit feedback from team members)
	- External Demo (python notebook at a min)
- Potential to de-scope the requirement based on research
	- Could be a timeline issue
	- Could be a cost issue
	- Might be able to solve part of the problem with more rigor
# Phase 3: Initial Production

- Scrum
- Should fit inside the timeline established in phase 2
- Getting security approval for additional software and models
- Periodic merge requests and reviews
	- Bring in a secondary team for outside feedback
- Engage outside stakeholders (development only)
- Integration with pre-existing services
# Phase 4: Sustainment

- Scrum
- Start over if expected hardware changes
- Publication potential
	- What avenues can we accomplish this?
- Teardown
