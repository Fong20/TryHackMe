
# Vulnerabilities 101

## Key Topics Covered:
- Definition of vulnerabilities
- Importance in cybersecurity
- Types of vulnerabilities
- Vulnerability management
- Vulnerability scoring (CVSS & VPR)
- Vulnerability research databases (NVD & Exploit-DB)

---

## What is a Vulnerability?

A **vulnerability** is a weakness or flaw in the design, implementation, or behavior of a system or application that can be exploited by an attacker to perform unauthorized actions or gain access to unauthorized information.

### Example Definition (NIST):
> "Weakness in an information system, system security procedures, internal controls, or implementation that could be exploited or triggered by a threat source."

---

## Types of Vulnerabilities

| Type                   | Description |
|------------------------|-------------|
| Operating System       | Found within OSs, often leads to privilege escalation. |
| (Mis)Configuration-based | Results from incorrectly configured apps or services. |
| Weak or Default Credentials | Default credentials like "admin:admin". |
| Application Logic      | Poorly designed app logic enabling user impersonation. |
| Human-Factor           | Social engineering tactics like phishing. |

---

## Vulnerability Management

- Involves evaluating, categorizing, and remediating threats.
- Not all vulnerabilities are worth patching — focus on the most dangerous.
- Only about **2%** of vulnerabilities are ever exploited.

---

## Vulnerability Scoring Systems

### Common Vulnerability Scoring System (CVSS)

- **Introduced**: 2005, current version: 3.1
- **Factors considered**: Ease of exploit, availability of exploits, CIA triad impact
- **Score Ranges**:
  | Rating   | Score     |
  |----------|-----------|
  | None     | 0         |
  | Low      | 0.1–3.9   |
  | Medium   | 4.0–6.9   |
  | High     | 7.0–8.9   |
  | Critical | 9.0–10.0  |

#### Advantages:
- Well-known and established
- Free and recommended by NIST

#### Disadvantages:
- Not intended for prioritization
- Scores static despite evolving threat context

---

### Vulnerability Priority Rating (VPR)

- **Developed by**: Tenable
- **Risk-driven**, dynamic, and organisation-specific
- **Score Ranges**:
  | Rating   | Score     |
  |----------|-----------|
  | Low      | 0.0–3.9   |
  | Medium   | 4.0–6.9   |
  | High     | 7.0–8.9   |
  | Critical | 9.0–10.0  |

#### Advantages:
- Considers 150+ risk factors
- Scores can change daily
- Helps prioritize patching

#### Disadvantages:
- Not open-source
- Requires commercial platform
- Less focus on CIA triad

---

## Vulnerability Research Resources

### Key Terms:
- **Vulnerability**: System weakness
- **Exploit**: Action using a vulnerability
- **Proof of Concept (PoC)**: Demonstrates how an exploit works

### National Vulnerability Database (NVD)
- Uses **CVE** format: CVE-YEAR-IDNUMBER (e.g., CVE-2017-0144)
- Tracks public vulnerabilities
- Useful for broad vulnerability tracking

### Exploit-DB
- Useful during assessments
- Contains PoC code and exploit details sorted by app/version/author
