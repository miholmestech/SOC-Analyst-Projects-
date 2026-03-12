## Header Analysis
The email headers were analyzed to identify sender infrastructure, authentication mechanisms, and potential anomalies. Header data was parsed using PhishTool to evaluate SPF/DKIM authentication results, originating IP information, and routing behavior.

The full email header used for this investigation is preserved in the

[email-sample.md](https://github.com/miholmestech/SOC-Analyst-Projects-/blob/main/03-email-phishing-triage-lab/01_email_sample.eml) file for reference and evidence integrity.


| Header Field | Value | Analyst Notes |
|---|---|---|
| From | nfo@tal-data.com | Appears legitimate at first glance but the domain requires reputation verification. |
| Return-Path | info@tal-data.com | Matches the sending domain, suggesting the email originated from infrastructure associated with the same domain. |
| Reply-To | newbeautymary@gmail.com | Redirects responses to an unrelated mailbox, a common tactic used in phishing or social engineering emails. |
| SPF | None | No SPF record exists for the sending domain, preventing verification of authorized sending servers. |
| DKIM | None | No DKIM signature detected, preventing validation of message integrity. |
| Originating IP | 77.68.73.179 | Investigated in VirusTotal; no security vendors currently flag the IP as malicious. |
| rDNS | None | The originating IP does not resolve to a hostname via reverse DNS lookup. Legitimate mail servers commonly have rDNS configured. |

---

## Key Observations

- The **Reply-To address differs from the sender domain**, redirecting responses to a Gmail account. This mismatch is a common indicator of phishing or social engineering attempts.

- The email **lacks both SPF and DKIM authentication mechanisms**, preventing verification of the sender's legitimacy.

- The originating IP **77.68.73.179 does not have reverse DNS configured**, which is uncommon for properly configured mail servers and may indicate suspicious infrastructure.

- Microsoft Exchange filtering assigned the email a **Spam Confidence Level (SCL) of 5**, indicating the message was already considered suspicious by the spam filtering system.

- The message body contains **vague language referencing a financial opportunity**, which is commonly used in advance-fee or reply-based phishing scams.

- Although the originating IP address is not currently flagged as malicious by security vendors, the combination of authentication gaps, reply-to mismatch, and social engineering language increases the likelihood that the email is fraudulent.

---

## Header Parsing Evidence

