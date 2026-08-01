# Case 001 — Microsoft Account Impersonation

**Date analysed:** June 2026  
**Analyst:** Dominika Bobkiewicz  
**Sample source:** rf-peixoto/phishing_pot (GitHub)  
**Verdict:** MALICIOUS — High Confidence

---

## Summary

A phishing email impersonating the Microsoft Account
Security Team, designed to trick recipients into
interacting via email rather than visiting a malicious
website. Instead of harvesting credentials through a
fake login page, the attacker uses **mailto** links to
confirm active email addresses for future phishing
attempts.

The investigation focused on analysing email headers,
authentication results, attacker infrastructure,
Indicators of Compromise (IOCs), and social engineering
techniques to determine whether the email was
legitimate or malicious.

---

## Email Header Analysis

| Field | Value | Finding |
|---|---|---|
| Display Name | Microsoft account team | Impersonating Microsoft |
| Sender | None verified | No legitimate sender confirmed |
| From domain | access-accsecurity.com | Fake lookalike domain — not microsoft.com |
| Reply-To | sotrecognizd@gmail.com | Attacker's Gmail inbox — flagged by PhishTool |
| Return-Path | bounce@thcultarfdes.co.uk | Unrelated UK domain used to send email |
| Originating IP | 89.144.44.2 | Polish server — not Microsoft infrastructure |
| rDNS | r2.mscode.pl | Polish domain — confirms non-Microsoft origin |

---

## Authentication Results

| Check | Result | Meaning |
|---|---|---|
| SPF | None | No SPF record configured |
| DKIM | Not verified | No valid signature present |
| DMARC | Fail | Email did not pass authentication |

**What this means:** A legitimate Microsoft email
would normally pass SPF, DKIM and DMARC validation.
Failing all three authentication checks is a strong
indicator of spoofing or unauthorised email delivery.

---

## Key Concepts Learned During This Investigation

### What is SPF?

SPF (Sender Policy Framework) is like a guest list
for email servers. The domain owner publishes which
servers are authorised to send email on their behalf.
If an email comes from a server not on that list,
SPF fails.

In this investigation, **thcultarfdes.co.uk** had
no SPF record configured, suggesting the domain was
created solely for phishing activity.

### What is DKIM?

DKIM (DomainKeys Identified Mail) works like a
tamper-proof seal on an email. It adds a digital
signature proving the message originated from the
claimed sender and was not modified in transit.

No valid DKIM signature was present, providing
further evidence that the email was not sent by
Microsoft.

### What is DMARC?

DMARC combines SPF and DKIM validation and defines
how receiving mail servers should handle messages
that fail authentication.

A DMARC failure indicates the message did not meet
the sending domain's own authentication policy.

### What is rDNS?

Reverse DNS (rDNS) performs the opposite function
of normal DNS by translating an IP address back into
a hostname.

The sender IP resolved to **r2.mscode.pl**, a Polish
host unrelated to Microsoft infrastructure, confirming
the message originated from attacker-controlled
systems.

### What is Email Harvesting?

Rather than directing victims to a fake login page,
this phishing campaign uses **mailto** links.

When the victim clicks either button, their email
client automatically prepares a message addressed to
the attacker. This confirms that:

- the mailbox is active
- the recipient interacted with the phishing email
- the attacker can continue targeting the victim

Because no website is involved, this technique can
evade automated URL scanning.

### Why does VirusTotal showing Clean not mean Safe?

Threat intelligence platforms rely heavily on
community reporting.

Attackers frequently register new domains and rotate
infrastructure before reputation databases can detect
them.

A "clean" result should never be treated as proof
that an email is safe. Header analysis, infrastructure
investigation and contextual evidence are far more
reliable.

---

## Indicators of Compromise (IOCs)

| Type | Value | Significance |
|---|---|---|
| Fake domain | access-accsecurity.com | Microsoft impersonation domain |
| Attacker email | sotrecognizd@gmail.com | Appears in Reply-To and both mailto buttons |
| Sending domain | thcultarfdes.co.uk | Infrastructure used to send phishing email |
| Sender IP | 89.144.44.2 | Polish server unrelated to Microsoft |
| rDNS | r2.mscode.pl | Confirms attacker infrastructure |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Initial Access | Phishing | T1566 |
| Initial Access | Spearphishing Link *(mailto interaction)* | T1566.002 |
| Credential Access | Email Harvesting *(potential follow-on objective)* | Observed behaviour |

---

## Attack Technique Analysis

**Technique:** Microsoft account impersonation via
email harvesting

**Primary tactic:** Social engineering using urgency
and fear to pressure victims into immediate action.

Instead of directing users to a phishing website,
the attacker encourages victims to communicate
directly via email, allowing future credential theft
through conversation.

### Button 1 — Report The User

| Field | Value |
|---|---|
| Link type | mailto |
| Destination | sotrecognizd@gmail.com |
| CC | sotrecognizd@gmail.com |
| Subject | unusual signin activity |
| Purpose | Confirms victim email address is active |

The button appears to let users report suspicious
activity but instead creates an email addressed to
the attacker.

---

### Button 2 — Unsubscribe

| Field | Value |
|---|---|
| Link type | mailto |
| Destination | sotrecognizd@gmail.com |
| CC | sotrecognizd@gmail.com |
| Subject | Unsubscribe me |
| Purpose | Confirms victim email address is active |

Although presented as an unsubscribe option, this
button has the same outcome as the first—confirming
that the victim's mailbox is active.

---

### Why no malicious URL?

Unlike traditional phishing campaigns, this attack
contains no malicious website links.

By relying entirely on **mailto** actions, the email
avoids URL reputation scanners and appears less
suspicious to automated security tools.

---

## Detection Opportunities

Security teams could detect similar phishing
campaigns by monitoring for:

- Microsoft display-name impersonation using non-Microsoft domains
- Reply-To domains differing from the From domain
- Messages failing SPF, DKIM and DMARC simultaneously
- Embedded **mailto** links inside security notifications
- Newly registered or low-reputation sender domains
- Infrastructure unrelated to the impersonated organisation

---

## VirusTotal Results

| IOC | Result | Notes |
|---|---|---|
| 89.144.44.2 | 0/91 Clean | Fresh infrastructure not yet reported |
| thcultarfdes.co.uk | Clean | Newly registered domain with no reputation |

---

## Investigation Timeline

```
Email received
        │
        ▼
Header analysis
        │
        ▼
Authentication review
        │
        ▼
Infrastructure investigation
        │
        ▼
IOC extraction
        │
        ▼
Threat assessment
        │
        ▼
Final verdict
```

---

## Lessons Learned

- SPF, DKIM and DMARC should always be analysed together.
- Email headers often reveal attacker infrastructure.
- Clean VirusTotal results do not prove an email is legitimate.
- Not all phishing campaigns use malicious websites.
- Infrastructure analysis provides stronger evidence than reputation alone.
- Multiple weak indicators, when correlated, can produce high-confidence findings.

---

## Verdict

| Field | Detail |
|---|---|
| Classification | Malicious — Phishing |
| Confidence | High |
| Attack type | Microsoft impersonation via email harvesting |
| Recommended action | Block sending domain, block Return-Path domain, report attacker Gmail account to Google, educate users not to interact with the email, and monitor for similar impersonation attempts |

---

## Tools Used

- PhishTool
- MXToolbox
- VirusTotal

---

## Screenshots

### PhishTool Analysis Panel
![PhishTool analysis](../screenshots/phishtool-analysis.png)

### Decoded Email — What the Victim Sees
![Decoded email](../screenshots/email-decoded.png)

### VirusTotal IP Check
![VirusTotal results](../screenshots/virustotal-ip.png)

---

*Sample source: github.com/rf-peixoto/phishing_pot*
