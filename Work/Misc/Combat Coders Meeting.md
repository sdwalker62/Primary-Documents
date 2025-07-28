---
created: 2025-07-18
attendees: James E Johnson, Robert B Cody, Alexander R Bailey, Nicholas D Montalbano
tags:
  - "#work"
  - "#dcgs"
---
# Notes

- Colonel Yang reached out to Alexander Bailey 
	- Combat Coders (held by Leidos)
		- They help the warfighter in gluing things together
		- Example:
			- Connecting UNICORN to ARCGIS
			- TMAN DB replication from UNICORN high to low
		- Want to make this more holistic across all of DCGS instead of just the current narrow scope
- Wants us to familiarize ourself with what the combat coders are doing right now so that we can help sustain these efforts
- Integrate some sort of generative coding for the analysts
	- Analyst A has an idea for something that can be scripted out
		- This is good for a one-off solution but not an enterprise solution
			- These are already going straight into production
				- Encapsulated by UNICORN
		- The analyst can do the level one coding of that
	- Sit with the analyst and see what they want out of this initiative
		- Show them how a LLM can code the initiative
- Go to DGS-1 to sit with Cpt. Prior and his team
- Cross over with high-side LLM development with A29-O?
- Best bang for our buck
	- This could be proprietary or organic
- Accept risk of running potentially two separate LLMs
	- Maybe Grok on low and another on high
		- Warn the analysts
- Aim would be for feature parity on both sides but it might be acceptable to not
- Deploy on the lowest level possible
	- Use one of the data diodes to push deployment up
- Could model off of the way ArcGIS where we deploy low and move up using the diode
- Col Rathamel? 

# Action Items

1. Alex will make a Confluence page that will be a repository of our knowledge, concerns, and questions on the matter.
2. Alex will setup a meeting with A29 since their efforts align with what we are doing.
3. Analyst Hackathon?
4. Add project information using LLMs 

# People

- **Alexander Bailey**
	- Working on the multi-int fusion engine
	- Large background in [[DCGS]]
		- Worked Systems Team in 577th
	- Helped install a lot of SIGINT DCGS capabilities
- **Nicholas Montalbano**
	- Started working with DCGS in 1999
	- Lockheed Martin for awhile
	- Worked with CACI
	- Involved in a large amount of projects
	- Less experience with GEOINT segment of DCGS
- **James Johnson**
	- With DGS-X since 2019
	- Worked with SOAESB, SOCET, and UNICORN
- **Robert Cody**
	- Chief engineer of DCGS
	- 

# Questions

1. What is the security posture around generated code.
2. What systems does the generated code touch?
3. Can adversaries take advantage of this code since the attack surface might be biased.
4. Can anyone generate code or only **trusted** developers?
5. What kind of LLMs are they running?
6. What IL level can they interface with?
7. Is automated code exporting modified data to a data lake? 
8. What does a CTF look like for generated code?