  

Same goal — very different lanes

  

  

All three programs exist to break data stovepipes inside the Department of the Air Force, but they grew up under different mission owners, handle very different data, and sit at different layers of the tech stack:

|   |   |   |   |
|---|---|---|---|
||Envision|Unified Data Library (UDL)|Mobility Enterprise Information Services (MEIS)|
|Sponsor / PMO|Chief Data & AI Office (CDAO) with SAF/CO, fielded on Palantir Foundry|Space Systems Command (BCCD) for US Space Force|Air Mobility Command / AFLCMC/HBM, aligned to USTRANSCOM|
|Core mission|Enterprise readiness, personnel, budget & analytics platform (e.g., UMD+, DAFLR, Brown Heron)|Cloud data-lake for Space Domain Awareness – ingests, normalises and republishes orbital sensor data|Service-oriented middleware for Mobility Air Forces C2, exposing flight-plan, airlift, refuelling & Total-Asset-Visibility feeds|
|Typical users|Unit commanders, A-staff shops, FM & HR analysts|Space Delta 2/18 SDS, JTF-SD, allied SSA centres, commercial SSA firms|618 AOC/TACC, 621 CRW, mission planners, GDSS & M2K operators|
|Data it owns|Authoritative feeds from MilPDS, myLearning, ACES, DEAMS, etc. (people + money)|Raw astrodynamics observations, orbital ephemerides, radar & EO tracks, conjunction alerts|Mission schedules, cargo status, aircrew/airframe status, C2 event messages|
|Layer in the stack|Applications + analytics + ontology + low-code app builder (Foundry Slate)|Data-exposure layer only – APIs, schemas, zero-trust tagging; UI-agnostic|Integration & messaging layer – SOA web services that other apps (GDSS, AvORM, MGOP) call|
|Deployment|NIPR & SIPR Foundry tenants; cell-level ABAC|Gov-owned AWS GovCloud; replicated to SIPR/JWICS; zero-trust guards|On-prem & GovCloud clusters; MEIS 3 migrating to MEIS 4 cloud|
|Security scope|PII/HR data—CAC gated|Unclassified thru TS/SCI via cross-domain guards|Unclass & Secret operational C2 data|

  

  

  

  

What this means in practice

  

  

- Envision = the place you build and view dashboards/apps  
    

- Low-/no-code tools, version-controlled pipelines, ontology; commanders can slice readiness or budget data and publish a Slate app in hours. The platform already tracks >59 k CBT records for 1.3 k Airmen at the 621 CRW alone  .

-   
    
- UDL = the clearing-house for space sensor data  
    

- Think “data broker.” It enforces common schemas, tags each record at ingest, and republishes via REST & Pub/Sub so any SDA tool can subscribe. It handles ~15 M observations/day, has ATOs at three classification levels and is now a formal Space Force Program of Record  .

-   
    
- MEIS = the plumbing behind AMC command-and-control  
    

- A service-oriented architecture that exposes air-mobility C2 and logistics data to GDSS and other mission apps. MEIS 3 hosts a catalog of “information/application services” that external consumers call for flight, aircrew and cargo status, and is being refactored as MEIS 4 in cloud  .

-   
    

  

  

  

  

  

Where they overlap (and don’t)

  

|   |   |
|---|---|
|Intersection|Reality on the ground|
|Data sharing between systems|Envision can consume UDL or MEIS feeds if a pipeline owner pulls them in, but there is no automatic replication. Each PMO owns its own ATO and metadata ontology.|
|User authentication|All three ride CAC/PKI and ABAC, so cross-tenant single-sign-on is technically possible, but today accounts are provisioned separately.|
|Analytics/AI|Envision provides built-in notebooks and AIP hooks; UDL and MEIS leave analytics to downstream tools.|
|Future convergence|CDAO’s Data Fabric vision calls for registering all authoritative sources (including UDL & MEIS) in a federated catalog, but that work is just starting.|

  

  

  

  

Quick cheat-sheet

  

  

- Ask yourself, “What data am I after?”  
    

- People, readiness, money → Envision
- Space objects & SSA → UDL
- Airlift C2 & mission execution → MEIS

-   
    
- Need dashboards? Use Envision.  
    UDL & MEIS feed other apps; they don’t render dashboards themselves.
- Need raw feeds or to publish a sensor? Talk to UDL (for space sensors) or MEIS (for mobility C2).

  

  

That separation of concerns is why the Air Force can run all three without duplicating effort—each tackles a different piece of the enterprise-data puzzle.