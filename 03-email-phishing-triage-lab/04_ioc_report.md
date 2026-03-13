# IOC Report

## Indicators of Compromise

| Indicator | Type | Description | Source |
|----------|------|-------------|--------|
| 77.68.73.179 | IP Address | Originating mail server used to send the email | Email Headers |
| solarjuice.co.uk | Domain | Mail server infrastructure used during message transmission | Email Headers |
| tal-data.com | Domain | Sender domain used in the email message | Email Headers |
| newbeautymary@gmail.com | Email Address | Reply-To address used to redirect responses outside the sending domain | Email Headers |

---

## Notes

The indicators listed above were extracted from the email headers and message metadata during analysis.  

While the originating IP address is not currently flagged as malicious by security services, the combination of authentication failures, reply-to redirection, and suspicious messaging behavior suggests the email is part of a phishing attempt.
