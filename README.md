🏥 VigiLens: Clinical Safety Command Center
Protecting Patients in a $50B Industry with Data Cloud + Tableau Next

"Time is Patient Safety."
VigiLens transforms scattered clinical trial safety signals into a prioritized risk leaderboard and triggers immediate, human-in-the-loop CAPA workflows directly in Salesforce.

📉 The Problem
Clinical trials run on trust. But in an ecosystem of hundreds of global sites, safety data (Adverse Events, Deviations, Logs) is often siloed in spreadsheets or external EDCs.

The Gap: By the time a safety monitor detects a trend using static reports, weeks have passed.

The Cost: Patient harm, delayed study timelines, and FDA warning letters.

💡 The Solution: VigiLens

VigiLens is a Closed-Loop Safety System that moves from Ingestion 
→→ Insight →→  Action →→
 Audit in under 60 seconds.
 
Architecture Overview

Ingestion: Raw CSV data (Sites, Patients, AEs) is ingested into Salesforce Data Cloud.
Harmonization: A custom Semantic Model links these objects, creating a unified view of risk.
Detection: Tableau Next visualizes the data, calculating a real-time Risk Signal Score for every site.
Action: A specific threshold breach (Score ≥ 15) alerts the user, who triggers a Salesforce Flow via a Deep Link to create a CAPA record.

⚙️ Key Features

1. The Risk Command Center (Tableau Next)
We moved beyond simple reporting to Decision Support.
Risk Signal Score: A custom metric calculated using Level of Detail (LOD) expressions to sum severity grades across Adverse Events and Deviations.
Dynamic Thresholds: A reference line at Score = 15 visually separates "Safe" sites from "Critical" sites (highlighted in Red).
Global Monitoring: Aggregates risk across hundreds of sites instantly.

3. "One-Click" CAPA Integration
Instead of switching tools, safety monitors take action directly from the dashboard.
Deep Linking: We utilize Tableau URL Actions to pass context parameters (Site Name, Risk Score, AE Counts) out of the dashboard.
Sanitized Data: Custom formulas STR(INT([Value])) ensure data types match strictly with Salesforce Flow variables.

5. Human-in-the-Loop Governance (Salesforce Flow)
Automated detection meets human decision-making.
Screen Flow: The user reviews the pre-filled safety data.
Audit Trail: Upon submission, a Risk_Action__c record is created in Salesforce CRM, timestamped and assigned for compliance tracking.

🛠️ Tech Stack & Implementation Details
Component	Usage
Salesforce Data Cloud	Data Ingestion (CSV), Data Lake Objects (DLOs), Data Modeling.
Tableau Next	Data Visualization, Calculated Fields, Dashboarding.
Semantic Model Builder	Defining Snowflake Schema relationships to avoid cyclic dependencies.
Salesforce Flow	Screen Flow for data capture and record creation logic.
Salesforce CRM	Custom Object (Risk_Action__c) for audit history.
Key Technical Challenges Solved
Cyclic Dependency Resolution: We structured the Data Cloud Semantic Model hierarchy to ensure Adverse_Event and Protocol_Deviation joined upstream to Patient and then Site to prevent model crash.
Data Type Strictness: Salesforce Flow failed when receiving decimal values from Tableau. We implemented explicit type casting in Tableau Calculated Fields to convert metrics to clean Integers before transmission.
