
# Classification: Malicious
Subtype: Financial Scam / Advance-Fee Fraud
Risk Level: High

## Key Indicators

DMARC failed (no alignment)**

DKIM not aligned with the From: domain

SPF passed but not aligned

“From:” domain (ProtonMail) does not match Gmail sending infrastructure

Free email provider used for impersonation

Multiple linguistic and formatting red flags

Claims of large financial compensation

No verifiable organization, identifiers, or professional branding


## Authentication Summary

**SPF**

Result: Pass

Alignment: Not aligned

SPF Domain: protonmail.com

Notes: Message routed through Gmail; authorized server but sender identity not validated

**DKIM**

Result: Fail

Reason: No DKIM signature aligned with the From: address

**DMARC**

Result: Fail

Reason: Alignment requirements not met; spoofing likely


## Final Rating

High Risk — Malicious Financial Scam

This message is a social engineering attempt impersonating a financial services entity to solicit engagement.
All authentication mechanisms fail alignment, and the content strongly matches known scam patterns.

Recommended Action

Block sender

Report as phishing

Add domain/address to filtering rules

Do not reply or engage
