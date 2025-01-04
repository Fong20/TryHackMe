
# AOC Day 2: Differentiating True Positives (TP) and False Positives (FP) in log analysis  
## **Key Concepts**  
### 1. **SIEM and Alert Workflow**  
- Events from multiple devices are aggregated in SIEM, which triggers alerts based on detection engineering rules.  
- SOC analysts determine if alerts are True Positives (actual threats) or False Positives (benign).  

### 2. **Importance of Accurate Classification**  
- Misclassifying TPs as FPs can result in missed attacks.  
- Misclassifying FPs as TPs wastes time and diverts resources.  

## **Guidelines for Analysis**  
### 1. **SOC Superpower**  
- Analysts can contact users for confirmation of activities.  
- Change Requests (CRs) in mature organizations can validate legitimate actions.  

### 2. **Context Building**  
- Analyze historical user behavior, event prevalence, and cross-departmental activity (e.g., network team vs. HR using Wireshark).  
- Identify anomalies or deviations from approved behaviors.  

### 3. **Correlation Techniques**  
- Recreate timelines using artifacts like IPs, user names, hashes, and process details.  
- Test hypotheses with evidence (e.g., process parent, command-line details).  

## **Case Study: Wareville SOC Investigation**  
### 1. **Incident Overview**  
- **Alert:** Encoded PowerShell commands executed across systems on Dec 1, 2024, between 0900-0930.  
- Authentication preceded commands, originating from a shared `service_admin` account.  

### 2. **Analysis Workflow**  
- **Initial Findings:** Commands executed from a suspicious source IP (10.0.11.11).  
- **Patterns:** Failed login spikes indicate brute-force attempts.  

### 3. **PowerShell Command Decoding**  
- Decoded with **CyberChef** (Base64 to UTF-16LE).  
- Revealed the intent was to fix outdated credentials, not malicious activity.  

### 4. **Key Findings**  
- Glitch, often perceived as a threat, helped secure systems by fixing credentials.  
- Misunderstood actions highlighted the complexity of TPs vs. FPs in SOC contexts.  

## **Lessons Learned**  
- Not all alerts are threats; investigation must consider intent and outcomes.  
- Historical evidence and correlation skills are vital for SOC analysts.  
- Effective communication and process adherence (e.g., CR validation) can reduce ambiguity.  
