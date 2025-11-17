These notes cover the entire initial phase of email analysis, focusing ONLY on:

Sender identity

Sending infrastructure

Authentication (SPF, DKIM, DMARC)

Server reputation

Sender URL (header-based)

This phase occurs before any analysis of message body links or attachments.

1. Basic Metadata

Example case analyzed:

Email ID: email-01
Date Received: 11-04-25
Folder: Inbox
Initial Suspicion: Low (Benign)

2. Quick Triage (60-Second Surface Check)
2.1 Sender & Identity Check

Does the sender match the From name?
No — “BrittanPickett@trugreenmail.com
” vs “emails@sales-exec.com
”

Is the domain real?
Yes — sales-exec.com is a real domain (VirusTotal: clean).
The site redirects to TruGreen (normal; ESP sending).

Is this impersonation?
No. The TruGreen employee is real and expected to contact me.

Dummy Proof Checks:

- Display name matches reply-to

- Domain spelled correctly

- This sender would contact me (I use TruGreen)

2.2 Subject Line

No urgency

No security-themed prompts

Contextually appropriate

2.3 Attachments or Links

No attachments

No links

Purpose matches body content (marketing)

2.4 Overall First Impression

Normal → Benign

3. Deep Analysis (Phase 1: Header & Identity)
3.1 Header Analysis

Tools used:

MXToolbox Email Header Analyzer

VirusTotal

IPinfo

Talos

AbuseIPDB

A. Return-Path — Who Actually Sent It
Return-Path: <bounces@em4053.sales-exec.com>


➡ Sender domain: sales-exec.com

This is controlled by the sending server/ESP.

B. Received Chain — Tracking Every Server Hop
Important Concept:

Read Received headers bottom → top.

Bottom-most = true origin

Top-most = final delivery (Yahoo/AOL)

Middle = routing (relays, ESPs, CRMs, marketing pipelines)

First “Received” line seen (NOT origin):
Received: from 127.0.0.1 
by atlas-production.v2-mail-prod1-gq1.omega.yahoo.com ...


This is:

✔ A hop

✔ INTERNAL to Yahoo

❌ NOT the origin

✔ “127.0.0.1” indicates local loopback

Conclusion:
This hop is irrelevant for sender legitimacy.

Workflow for confirming the true sending server

Bottom-most Received = origin
Top-most Received = mailbox delivery

To confirm the sender:
(1) Copy hostname from Received header

Example:

Received: from 168.245.19.130 (EHLO o1.ptr7709.sales-exec.com)


Hostname patterns to look for:

SendGrid → geopod- / ismtp- / recvd-canary

Mailgun → mxa.mailgun.org

SES → amazonses.com

Mandrill/Mailchimp → mandrillapp.com

Salesforce/Pardot → sales-exec.com

Check:

Does hostname look real?

Machine-generated or human-friendly?

Does it match known ESP patterns?

(2) Paste hostname/IP into MXToolbox

What to check:

Does it resolve normally?

Does MXToolbox label it as an ESP?

Blacklist status

Spam history

Server owner

(3) Paste IP into IPinfo or VirusTotal

Check:

Org/ISP (SendGrid, Mailgun, Salesforce, AWS, etc.)

ASN

Reputation

Hosting type (cloud, residential, VPS)

(4) Match patterns to known ESP signatures

Examples:

SendGrid

geopod-

ismtp-

recvd-canary

sendgrid.net in SPF

Mailgun

mxa.mailgun.org

mxb.mailgun.org

AWS SES

amazonses.com

Salesforce/Pardot

sales-exec.com (your case)

This confirms commercial email marketing infrastructure.

(5) Check protocol in bottom-most Received header

"with HTTP" → API submission (marketing, CRM automations)

"with SMTP" → user mailbox / corporate mailserver

This email shows API submission — consistent with marketing automation (TruGreen).

C. Server Reputation Analysis (OSINT Stack)
1. MXToolbox (initial reputation)

Checks:

Blacklists

SMTP diagnostics

Spam score

ESP fingerprint

2. Cisco Talos (threat reputation)

Checks:

Malicious / suspicious / neutral / benign

Spam campaigns

Botnet affiliation

Abuse patterns

3. IPinfo / WHOIS

Checks:

Server owner

Infrastructure type (cloud, VPS, business)

Expected vs unexpected origin

4. AbuseIPDB

Checks:

User-submitted abuse

Phishing

Brute-force attempts

Botnet activity

Conclusion (Server):

All indicators consistent with SalesExec → TruGreen marketing pipeline.
Reputation clean.

3.2 Authentication Results (SPF, DKIM, DMARC)

Located under:

Authentication-Results:


Before interpreting, identify the sending server FIRST (done above).

SPF: pass

IP authorized to send for domain.

DKIM: pass

Cryptographic signature valid.

DMARC: pass

SPF/DKIM aligned with “From” domain.

Rules of Thumb

Fail + login request → High risk

Pass + weird content → possible compromised sender

All fail → spoofing attempt

3.3 Sender URL Analysis (Header Only)

This step focuses ONLY on identifying the sender’s domain identity, not body links.

The sender’s URL (domain) appears in four header locations:
1. Return-Path

Most reliable.

2. SPF MAILFROM Domain

Found under “Received-SPF: domain of…”

3. DKIM d= Domain

Found under “dkim=pass … d=…”

4. Sending Server Hostname (Received headers)

Shows infrastructure domain.

Summary Principle

The sender’s URL is obtained from Return-Path, SPF MAILFROM, DKIM d=, or the sending server hostname.
This identifies who actually sent the message.
This stage does NOT evaluate clickable links.

Mismatches may indicate:

Forwarding

ESP (legitimate)

Spoofing

Delegated marketing

Misconfiguration

Malicious sending

Summary Conclusion
Sender identity, infrastructure, reputation, and authentication all point to:

- Legitimate TruGreen marketing email
- Sent via SalesExec (Salesforce/Pardot-type ESP)
- No malicious indicators
- Passed all authentication
- Normal content and expected sender
