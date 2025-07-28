ODIN = Operations Dedicated Imagery Network

|   |   |
|---|---|
|Key point|What it means for the Air Force|
|Mission|Moves large-volume overhead and tactical imagery (satellite stills, synthetic-aperture radar products, full-motion video, annotated target graphics, etc.) from national/intelligence community sources and Air Force Distributed Common Ground System (AF-DCGS) sites down to operational users (Air Operations Centers, wings, and in-theater headquarters).|
|Pedigree|Built in the 1990s as the imagery “back-bone” inside NATO’s Linked Operations Intelligence Center–Europe (LOCE) architecture and later folded into the Joint Deployable Intelligence Support System (JDISS) family. It remains the imagery segment of LOCE today.|
|Security level|Collateral SECRET//REL NATO (or other coalition) enclave. It rides the Defense Information Systems Network (DISN) but is logically separate from NIPRNet (unclassified) and SIPRNet (general DoD Secret traffic). SCI/Top-Secret imagery still moves over JWICS; ODIN handles “collateral Secret” and releasable feeds.|
|Typical users|• 603rd AOC (Ramstein), 612th AOC (Davis-Monthan), 609th AOC (Al Udeid), 613th AOC (Hickam)|
|• 480th ISR Wing DCGS nodes||
|• Allied air staffs plugged into LOCE (RAF High Wycombe, CAOC Uedem, etc.)||
|Why a separate network?|Moving imagery is bandwidth-intensive and latency-sensitive. ODIN gives planners and targeteers a “fat pipe” that doesn’t bog down command-and-control chat or fires data flowing on SIPRNet.|
|Typical services running on ODIN|• JDISS/Joint Worldwide Intelligence Communication System (JWICS) “push-down” mirrors at collateral level|
|• NGA GETS & NIL imagery servers (Secret)||
|• FalconView/CFPS map tile repositories||
|• STANAG-compliant motion-imagery servers for RQ-4, MQ-9, U-2 feeds||

  

  

  

  

How it fits with other Air Force/DoD networks

  

|   |   |   |   |
|---|---|---|---|
|Network|Classification|Primary content|Quick differentiator|
|NIPRNet|Unclassified (but DoD only)|Email, Web, routine logistics|Everyday garrison traffic|
|SIPRNet|Secret (US only)|Planning chat, C2 apps, intel text|“Main street” Secret network|
|ODIN|Secret // Releasable coalition|Large imagery & video|Optimized for GEOINT bulk data|
|JWICS|Top Secret / SCI|Sensitive compartmented intel|SCI & “national” sources|
|DREN/SERN|Unclassified & Secret R&D|DoD research, test data|Lab/test-range focused|
|F-35 “ODIN” logistics cloud|Unclassified-to-Secret|Maintenance & supply data|Different acronym – Operational Data Integrated Network|

  

  

  

  

Common mix-ups

  

  

1. ODIN (Operations Dedicated Imagery Network) – what you asked about; an intel transport network.
2. ODIN (Operational Data Integrated Network) – new cloud-native replacement for the F-35’s Autonomic Logistics Information System (ALIS); unrelated to imagery.  
3. Task Force ODIN – Army aviation battalion (“Observe, Detect, Identify, Neutralize”) that flies ISR drones; again, unrelated.  

  

  

  

  

  

Why you might encounter ODIN in Air Force work

  

  

- Target development: Analysts at an Air Operations Center pull National Geospatial-Intelligence Agency (NGA) products over ODIN so weaponeers can build precise aim-points.
- ISR processing: After an RQ-4 Global Hawk mission, the AF-DCGS site processes raw imagery and republishes finished graphics and video clips onto ODIN for coalition planners.
- Coalition sharing: Because it is REL NATO, ODIN is the fastest legal way to move Secret imagery to allied targeting cells without resorting to file-transfer kludges on SIPR.

  

  

  

  

  

Bottom line

  

  

Think of ODIN as the Air Force’s (and NATO’s) purpose-built, Secret-level “fast lane” for high-volume imagery, sitting beside—but not replacing—SIPRNet and JWICS. It keeps GEOINT flowing to crews and planners who need pictures now, without clogging the other operational networks.