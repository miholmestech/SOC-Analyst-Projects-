# Detection Logic

## Objective

Detect suspicious emails that attempt to impersonate a legitimate sender while redirecting responses to a different mailbox.

## Detection Conditions

The following conditions may indicate a phishing attempt:

- Reply-To address does not match the sender domain
- Missing email authentication mechanisms (SPF, DKIM, or DMARC)
- Suspicious infrastructure or unknown sending IP
- Vague or unsolicited financial messaging

## Example Detection Logic (Pseudocode)

```
IF email.reply_to_domain != email.from_domain
AND (dkim == none OR spf == softfail OR spf == none)
THEN
flag email as suspicious
generate alert for SOC review

```

## Potential SIEM Fields

The following email metadata fields may be useful when building detection logic:

- email.from
- email.reply_to
- email.return_path
- email.source_ip
- email.authentication_results

Monitoring these fields can help identify emails that exhibit common phishing behaviors such as sender impersonation or reply redirection.
