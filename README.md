# Phishing Email Analysis Lab

A hands-on cybersecurity portfolio documenting phishing email investigations completed as part of my preparation for a SOC Analyst role.

Each case study analyses a real phishing email sample using industry-standard investigative techniques to determine whether the email is legitimate or malicious. Investigations focus on email authentication, attacker infrastructure, Indicators of Compromise (IOCs), social engineering techniques, and evidence-based threat assessment.

---

# Investigation Methodology

Every investigation follows a structured SOC-style triage workflow:

1. Analyse email headers (From, Reply-To, Return-Path, Message-ID, Received headers)
2. Validate SPF, DKIM and DMARC authentication
3. Investigate attacker infrastructure (domains, sender IP addresses and reverse DNS)
4. Extract and document Indicators of Compromise (IOCs)
5. Analyse the email body and identify phishing techniques
6. Correlate findings using threat intelligence platforms
7. Assess evidence and assign a confidence-based verdict
8. Recommend defensive actions and detection opportunities

---

# Case Studies

| Case | Email Subject | Verdict | Attack Technique |
|------|---------------|----------|------------------|
| Case 001 | Microsoft account unusual signin activity | **Malicious** | Microsoft impersonation via email harvesting |

---

# Tools Used

- **PhishTool** — email parsing, decoding and header analysis
- **MXToolbox** — email authentication and DNS analysis
- **VirusTotal** — IP and domain reputation analysis
- **URLScan.io** — URL investigation (where applicable)
- **Base64Decode.org** — email body decoding

---

# Skills Demonstrated

## Email Security

- Email Header Analysis
- Email Authentication Analysis
- SPF
- DKIM
- DMARC

## Threat Investigation

- Phishing Analysis
- Threat Analysis
- Indicators of Compromise (IOC) Identification
- Attacker Infrastructure Analysis
- Reverse DNS (rDNS) Investigation
- Domain Reputation Analysis
- IP Reputation Analysis

## Defensive Analysis

- Social Engineering Analysis
- Threat Intelligence Correlation
- Confidence-Based Threat Assessment
- Security Recommendations
- Detection Opportunity Identification

## Documentation

- SOC Investigation Reporting
- Technical Documentation
- Evidence-Based Analysis

---

# Repository Structure

```
Phishing-Email-Analysis-Lab/
│
├── README.md
│
├── cases/
│   └── case-001-microsoft-account-impersonation/
│       ├── README.md
│       └── screenshots/
│
└── screenshots/
```

---

# Current Investigations

## Case 001 — Microsoft Account Impersonation

**Summary**

Analysed a phishing email impersonating the Microsoft Account Security Team. The investigation identified a mailto-based email harvesting campaign that used urgency and social engineering instead of malicious URLs to confirm active email addresses.

**Key investigation activities**

- Email header analysis
- SPF, DKIM and DMARC validation
- Attacker infrastructure investigation
- IOC extraction and documentation
- Email harvesting technique analysis
- Threat intelligence correlation
- High-confidence phishing verdict
- Recommended defensive actions

---

## Disclaimer

All investigations are performed on publicly available phishing samples for educational and research purposes only. No live attacks were conducted, no production systems were targeted, and no real victims were involved.
