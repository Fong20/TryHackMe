# MISP 

## Overview  
- **MISP (Malware Information Sharing Platform)** is an open-source threat intelligence platform.  
- Facilitates collection, storage, and distribution of threat intel & Indicators of Compromise (IOCs).  
- Supports closed, semi-private, and open (public) communities.  
- Integrates with:  
  - **NIDS** (Network Intrusion Detection Systems)  
  - **Log analysis tools**  
  - **SIEMs** (Security Information & Event Management systems)  

---

## Use Cases
- **Malware Reverse Engineering** – Sharing malware indicators.  
- **Security Investigations** – Searching, validating, and using IOCs.  
- **Intelligence Analysis** – Adversary group tracking.  
- **Law Enforcement** – Forensics and investigation support.  
- **Risk Analysis** – Researching new and emerging threats.  
- **Fraud Analysis** – Detecting financial fraud.  

---

## Core Functionalities
- **IOC Database** – Stores technical/non-technical info.  
- **Automatic Correlation** – Identifies relationships between attributes.  
- **Data Sharing** – Different distribution models across MISP instances.  
- **Import/Export Features** – Supports formats for NIDS, HIDS, OpenIOC, etc.  
- **Event Graph** – Visual representation of relationships between objects/attributes.  
- **API Support** – Fetch/export events programmatically.  

---

## Key Terminology
- **Events** – Contextually linked information.  
- **Attributes** – Individual data points (e.g., IPs, hashes).  
- **Objects** – Custom attribute groupings.  
- **Object References** – Relationships between objects.  
- **Sightings** – Time-specific occurrences of attributes.  
- **Tags** – Labels for events/attributes.  
- **Taxonomies** – Classification libraries for organizing data.  
- **Galaxies** – Knowledge base items to label events/attributes.  
- **Indicators** – Detect malicious/suspicious activity.  

---

## Dashboard Navigation
- **Home** – Start screen or custom home.  
- **Event Actions** – Create, edit, delete, publish, search, list events & attributes.  
- **Dashboard** – Customizable with widgets.  
- **Galaxies** – Shortcut to knowledge base.  
- **Input Filters** – Regex replacements, blocklists, validation.  
- **Global Actions** – Profile, manual, news, active orgs, histograms.  
- **MISP Link** – Base URL.  
- **User Panel** – Notifications, proposals, log out.  

---

## Event Management Workflow
1. **Event Creation**  
   - Add description, time, risk level.  
   - Choose distribution:  
     - Organisation only  
     - Community only  
     - Connected communities  
     - All communities  
   - Optionally add **Sharing Groups**.  

2. **Attributes & Attachments**  
   - Add manually or import (OpenIOC, ThreatConnect).  
   - **Intrusion Detection System flag** → attribute usable in IDS.  
   - **Batch Import** → multiple attributes in one entry (newline separated).  
   - Attach files (malware, reports, artefacts).  
   - Malware files are **zipped + password-protected**.  

3. **Publishing**  
   - Admin reviews & publishes events.  
   - Shares with set distribution channels.  

---

## Feeds
- Sources containing indicators & attributed event information.  
- Provide continuously updated intel.  
- Enable:  
  - Threat info exchange  
  - Event preview/import  
  - Correlation of attributes  
- Managed by **Site Admin**.  

---

## Taxonomies
- Classification system using **tags**.  
- Expressed in **machine tags**:  
  - **Namespace** – Tag’s property  
  - **Predicate** – Property type  
  - **Value** – Text/number value  

**Analyst Use Cases:**  
- Set events for external processing (e.g., VirusTotal).  
- Classify events before publishing.  
- Enrich IDS exports.  

---

## Tagging
- Tags applied at **event or attribute level**.  
- Inheritable (event → attributes).  
- Analysts/organizations can create **custom tags**.  

### Best Practices
- **Event-level tagging preferred**, unless exceptions exist.  
- **Minimal subset of tags:**  
  - **Traffic Light Protocol (TLP)** – Sharing guidelines.  
  - **Confidence** – Quality & vetting of data.  
  - **Origin** – Source of information (manual/automated).  
  - **Permissible Actions Protocol** – Defines allowed data usage.  
