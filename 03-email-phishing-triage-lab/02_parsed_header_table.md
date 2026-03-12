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

The following screenshots document the email header analysis performed using PhishTool. These images illustrate the sender metadata, authentication results, and transmission path used to deliver the message.

---

### Email Metadata

![Email Metadata](images/01-phishtool.png)

This view shows the core email metadata including the sender address, display name, reply-to address, and message identifier.

Notable finding:
- The **Reply-To address (newbeautymary@gmail.com)** differs from the sender domain (tal-data.com), indicating responses would be redirected to an unrelated mailbox.

---

### Email Transmission Path

![Transmission Path](images/02-phishtool.png)

This view shows the email routing path through multiple mail servers before reaching the recipient.

Key observation:
- The message originated from **solarjuice.co.uk** infrastructure before being processed by **Microsoft Exchange Online Protection**.

---

### Email Routing Hops

![Routing Hops](images/03-phishtool.png)

The hop sequence shows the message traveling through multiple Microsoft mail protection systems before reaching the recipient mailbox.

This indicates the email was processed by **Microsoft's spam filtering infrastructure**.

---

### Authentication Results

![Authentication Results](images/05-phishtool.png)

Authentication analysis shows:

- **No SPF record published for the sending domain**
- **No DKIM signature present**
- **No reverse DNS (rDNS) configured for the originating IP**

These missing authentication mechanisms prevent verification of the sender's legitimacy.

---

### Microsoft Spam Filtering Evidence

![Spam Confidence Level](images/06-phishtool.SCL.png)

The raw headers reveal:
X-MS-Exchange-Organization-SCL: 5
This indicates Microsoft's spam filtering system assigned the message a **Spam Confidence Level (SCL) of 5**, meaning the email was considered **likely spam** by Exchange Online Protection.

