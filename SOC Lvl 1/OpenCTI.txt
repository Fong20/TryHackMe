# OpenCTI  

## Overview  
- **OpenCTI**: Open-source threat intelligence platform for storing, analyzing, visualizing, and presenting threat campaigns, malware, and IOCs.  
- **Objective**: Developed by ANSSI (French National Cybersecurity Agency).  
  - Provides comprehensive CTI management.  
  - Structures data with **MITRE ATT&CK** framework.  
  - Integrates with **MISP** and **TheHive**.  

## Data Model  
- Uses **STIX2 standard** for structured threat intelligence exchange.  
- Data is represented as **entities + relationships**, allowing traceability to sources.  

## Architecture  
- **GraphQL API**: Connects clients to DB & messaging system.  
- **Write Workers**: Python processes writing queries asynchronously from RabbitMQ.  
- **Connectors**: Python processes for ingesting, enriching, exporting data.  

### Connector Types  
| Class                        | Description                               | Examples                 |  
|-------------------------------|-------------------------------------------|--------------------------|  
| External Input Connector      | Ingest external sources                   | CVE, MISP, TheHive, MITRE |  
| Stream Connector              | Consume platform data streams             | History, Tanium          |  
| Internal Enrichment Connector | Enrich OpenCTI entities from user input   | Observables enrichment   |  
| Internal Import File Connector| Extract info from uploaded files          | PDFs, STIX2 import       |  
| Internal Export File Connector| Export data into various formats          | CSV, STIX2 export, PDF   |  

## Dashboard  
- Widgets summarize threat data:  
  - Number of entities, relationships, reports, observables.  
  - Changes within 24h.  

## Key Navigation Areas  

### Activities & Knowledge  
- **Activities**: Security incidents in form of reports → investigation.  
- **Knowledge**: Linked data (tools, victims, threat actors, campaigns).  

### Analysis  
- Central to threat investigation.  
- Reports contain input entities, external references, analyst notes.  

### Events  
- Records suspicious/malicious activity findings.  
- Helps enrich threat intel by creating associations.  

### Observations  
- Lists technical elements (IOCs, detection rules, artifacts).  
- Used for threat hunting and correlation.  

### Threats  
- **Threat Actors**: Individuals/groups with malicious intent.  
- **Intrusion Sets**: TTPs, tools, malware used repeatedly (e.g., APTs).  
- **Campaigns**: Series of attacks by APTs with objectives.  

### Arsenal  
- **Malware**: Details on known malware & trojans.  
- **Attack Patterns**: TTPs adversaries use.  
- **Courses of Action (CoA)**: Mitigations from MITRE.  
- **Tools**: Legitimate tools (also abused by attackers).  
- **Vulnerabilities**: CVEs & weaknesses (ingested via connector).  

### Entities  
- Categorized by sectors, countries, organizations, individuals.  
- Provides knowledge enrichment context.  

## Entity Details Navigation  
- **Overview Tab**: General info (ID, confidence, relations, reports, refs).  
- **Knowledge Tab**: Linked info (reports, indicators, attack patterns).  
- **Analysis Tab**: Reports referencing the entity.  
- **Indicators Tab**: IOC details.  
- **Data Tab**: Uploaded/generated files for communication.  
- **History Tab**: Tracks changes to attributes & relations.  
