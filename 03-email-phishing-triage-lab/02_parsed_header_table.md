
## Header Analysis

The email headers were analyzed to identify sender infrastructure, authentication mechanisms, and potential anomalies. Header data was parsed using PhishTool to evaluate SPF/DKIM authentication results, sender domains, and routing information.

| Header Field | Value | Analyst Notes |
|---|---|---|
| From | nfo@tal-data.com | Appears legitimate at first glance but the domain requires reputation verification. |
| Return-Path | info@tal-data.com | Matches the sending domain, suggesting the email originated from the same infrastructure. |
| Reply-To | newbeautymary@gmail.com | Redirects responses to an unrelated mailbox, a common tactic used in phishing or social engineering emails. |
| SPF | None | No SPF authentication record present for the sending domain, preventing verification of authorized senders. |
| DKIM | None | No DKIM signature detected, preventing validation of message integrity. |
| Originating IP | 77.68.73.179 | Investigated in VirusTotal; no security vendors currently flag the IP as malicious. |

---

## Key Observations

- The **Reply-To address differs from the sender domain**, redirecting responses to a Gmail account. This mismatch is a common indicator of phishing or social engineering attempts.

- The email **lacks both SPF and DKIM authentication records**, preventing verification of the sender's legitimacy and weakening trust in the message source.

- The message body contains **social engineering language referencing a financial opportunity**, which is a common tactic used in advance-fee or phishing scams.

- Although the **originating IP address is not currently flagged as malicious**, the absence of authentication mechanisms combined with suspicious messaging increases the likelihood that the email is fraudulent.

---

## Header Parsing Evidence

![PhishTool Header Analysis](images/phishtool-header-analysis.png)
