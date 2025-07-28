  

Cloud-Based Command & Control (CBC2)

  

|   |   |
|---|---|
|Item|Details|
|Program owner|Department of the Air Force (DAF) — Program Executive Office, Command, Control, Communications & Battle Management (PEO C3BM).|
|What it is|A cloud-native battle-management/command-and-control (BMC2) software suite that fuses data from >700 sensors (radars, ADS-B, LINK-16, etc.) into a single, zero-trust environment, then uses analytics/AI to recommend courses of action. Originally targeted at NORAD & USNORTHCOM homeland-air-defense missions, CBC2 is one of the first operational “apps” inside the DAF’s Advanced Battle Management System (ABMS) architecture.|
|How it works|• Runs in Cloud One / Platform One DevSecOps pipelines, delivered as micro-services that can update in minutes instead of months. • Accessible from laptops, mobile devices, and emerging Tactical Operations Center-Light (TOC-L) kits. • Built to a zero-trust reference design so that upgrades or third-party AI/ML “plug-ins” can be fielded rapidly.|
|Fielding status (Jul 2025)|• IOC Oct 2023 at Eastern Air Defense Sector (EADS). • By Sep 2024 CBC2 had been rolled out to all six U.S. & Canadian air-defense sectors﻿ . • Continuous agile sprints are adding features every ~12 weeks ﻿ .|

  

  

  

  

CBC2 

“Plus”

 (CBC2+)

  

|   |   |
|---|---|
|Item|Details|
|Why “+” ?|CBC2+ is the follow-on modernization line in the FY-26 RDT&E budget.  Where baseline CBC2 focused on fixed homeland-defense sites, **CBC2+ broadens the software and data fabric so it can power expeditionary, highly mobile, or coalition C2 nodes (e.g., Tactical Operations Center-Light).  Budget justification language frames it as “the newly-named CBC2+ program,” nested under the C3BM Software & Applications thrust ﻿ .|
|Key additions|* TOC-L enablement. CBC2+ funds the APIs, security enclaves, and lightweight compute stack so the same battle-management picture can run on a palletized TOC-L module that two Airmen can set up in < 60 min ﻿ .* Higher-classification hosting. Extends the data-fabric to TS/SCI enclaves and coalition releasable domains.* Dispersed ops & Degraded comms. Adds edge-sync and store-and-forward services so nodes can keep fighting through disconnections.* Weapon-tasking services. Integrates fires and counter-UAS orchestration so operators can “close the kill chain” directly from the same UI.|
|Acquisition path|Planned as a Software Acquisition Pathway; first operational test events are aligned with Project Convergence Capstone 5 and PACAF Agile Combat Employment exercises in FY-26–27.|
|Relationship to ABMS|CBC2+ remains an ABMS component program of record, but its budget line is now shared with other BMC2 “apps” to encourage code reuse and a common data-mesh.|

  

  

  

  

Quick comparison

  

|   |   |   |
|---|---|---|
|Feature|CBC2 (baseline)|CBC2+ (increment)|
|Primary mission|Fixed-site NORAD air-defense sectors|Mobile & expeditionary C2 (TOC-L, ACE)|
|Deployment|Cloud One IL-5/6 GovCloud regions|Adds edge compute kits, future IL-7|
|Sensor feeds|>700 air-radar & FAA tracks|Same + space, maritime & ground sensors|
|Data-sharing|U.S. & Canadian operators|Adds coalition releasability & CJADC2 data-mesh|
|Milestones|IOC 2023, full NORAD fielding 2024|First OT events FY-26; IOC goal FY-27|

  

  

  

  

Why it matters

  

  

- Speed to decision: Early operational testing showed a 30–50 % reduction in operator “detect-to-decide” timelines versus legacy scopes.
- DevSecOps precedent: CBC2 proved that large-scale classified C2 can be delivered like commercial SaaS; CBC2+ will push that model to the tactical edge.
- Building block for CJADC2: By normalizing APIs and data formats, the “+” increment is designed to let Army IBCS, Navy NIFC-CA, and Marine Project Tripoli apps plug into the same data fabric.

  

  

  

  

Bottom line:  CBC2 gives NORAD a modern, cloud-native air-defense picture today.  CBC2+ is the budgeted expansion that turns that same software into a portable, coalition-ready C2 stack capable of running anywhere the joint force needs it—from a permanent operations center in Colorado to a two-person TOC-L shelter on a Pacific island.