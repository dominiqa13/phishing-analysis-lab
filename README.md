# Phishing Email Analysis Lab

Hands-on phishing email investigation and analysis 
practised as part of my SOC analyst preparation.

Each case documents a real phishing email sample 
investigated using industry-standard tools and 
methodology — the same process used by Tier 1 
SOC analysts in real security operations centres.

---

## Investigation Methodology

Every case follows this structured triage process:

1. Analyse email headers — From, Reply-To, Return-Path
2. Check SPF, DKIM, DMARC authentication results
3. Identify originating IP and run reverse DNS lookup
4. Check IOCs against VirusTotal and URLScan.io
5. Decode email body and identify malicious content
6. Document all IOCs and make a verdict

---

## Cases

| Case | Email Subject | Verdict | Technique |
|---|---|---|---|
| Case 001 | Microsoft account unusual signin activity | Malicious | Microsoft impersonation via email harvesting |

---

## Tools Used

- PhishTool — email analysis and decoding
- MXToolbox — email header analysis
- VirusTotal — IP and domain reputation checking
- URLScan.io — safe URL investigation
- base64decode.org — email body decoding

---

## Skills Demonstrated

- Email header analysis and authentication checking
- SPF, DKIM, DMARC interpretation
- IOC identification and documentation
- Phishing technique classification
- Professional investigation report writing
- Triage verdict and confidence assessment

---

*All analysis performed on phishing samples from 
public research collections for educational purposes. 
No real victims or live systems involved.*
