---

# Phishing Analysis Report

---

## Incident Summary

A suspicious email sample was selected from the **rf-peixoto phishing dataset** for analysis. The message was reviewed to determine whether it exhibited characteristics of a phishing attempt.

As part of the investigation, the email headers were parsed to identify sender infrastructure and authentication results. Embedded domains and message content were analyzed using public threat intelligence tools to identify potential indicators of compromise (IOCs).

The goal of this analysis is to determine whether the message represents a phishing attempt and document relevant findings, indicators, and potential detection opportunities.

---

## Findings

Header analysis revealed that the email lacks **SPF, DKIM, and DMARC authentication mechanisms**, preventing verification of the sender’s legitimacy. The message was transmitted through the mail server **solarjuice.co.uk (77.68.73.179)** before passing through Microsoft Exchange Online Protection infrastructure.

The email content contains vague language referencing a financial opportunity, which is a common **social engineering tactic used in advance-fee phishing scams**. Additionally, the message redirects responses to a different **Reply-To address**, which may be used to collect responses outside of the original sending domain.

Upon reviewing the email headers, Microsoft Exchange filtering assigned the message a **Spam Confidence Level (SCL) of 5**, indicating that the email was already considered suspicious by the spam filtering system.

Although the originating IP address is not currently flagged as malicious by security vendors, the combination of **missing authentication controls, reply-to mismatch, an SCL score of 5, and social engineering language** indicates that the message is likely part of a phishing attempt.

The email sample was also submitted to VirusTotal for additional analysis. No security vendors flagged the file as malicious and sandbox analysis did not identify malicious behavior. This result is consistent with reply-based phishing scams that rely on social engineering rather than malware delivery.

**Conclusion:** Based on the observed indicators and header analysis, the email is assessed as a likely phishing message.

---

## Attack Techniques

**Social Engineering**

The email contains vague language suggesting a financial opportunity. This style of messaging is commonly used in **advance-fee or reply-based phishing scams**, where attackers attempt to initiate a conversation with the recipient rather than directing them to a malicious link.

**Email Spoofing / Reply Redirection**

The email uses a sender address associated with the domain `tal-data.com` but redirects responses to an unrelated Gmail account (`newbeautymary@gmail.com`). This mismatch is a common indicator of phishing or impersonation attempts.

---

## Mitigation

- Block or monitor the sending infrastructure associated with the message.
- Implement email authentication protections such as **SPF, DKIM, and DMARC** to improve sender verification.
- Educate employees to avoid responding to unsolicited messages requesting sensitive information or financial discussions.
- Encourage users to report suspicious emails to the security team for investigation.

---
