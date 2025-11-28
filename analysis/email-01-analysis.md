## 1.1 Bottom-Most “Received” Header (True Origin)

Field	Value
Hostname	o1.ptr7709.sales-exec.com
IP Address	168.245.19.130
Protocol	HTTP
Infrastructure Type	ESP (SendGrid)

Interpretation:

Hostname is human readable → matches ESP formatting.

IP belongs to SendGrid, not the corporate domain.

HTTP indicates API-based sending (automation).

<img width="429" height="75" alt="email-01-bottom-received " src="https://github.com/user-attachments/assets/fc78932f-0224-49b2-8728-6f1f909b8dd4" />


## 1.2 Hostname Ownership (MXToolbox Lookup)

Field	Value
Hostname	o1.ptr7709.sales-exec.com
Resolution	Yes
Provider	SendGrid (Twilio)
Blacklist Status	Clean

Interpretation:
Hostname resolves correctly and is clean across blacklists.

<img width="692" height="133" alt="image" src="https://github.com/user-attachments/assets/b22d679f-4c91-4a1b-a726-82cce85adfc6" />



<img width="926" height="635" alt="image" src="https://github.com/user-attachments/assets/1a13010f-69f0-4ec5-8bbc-873b4315ae5b" />



## 1.3 IP Ownership (VirusTotal)

Field	Value
IP	168.245.19.130
Owner / ISP	SendGrid / Twilio
ASN	AS11377
IPinfo Reputation	Clean
VirusTotal Reputation	0/90 flagged

Interpretation:
Matches major ESP infrastructure and shows no abuse detections.

<img width="782" height="470" alt="email-01-virustotal-ip" src="https://github.com/user-attachments/assets/5318f109-6328-4253-b99c-67b7f38639bc" />





## 1.4 ESP Pattern Validation (SendGrid)
Evidence Type	Value
DKIM d=	sendgrid.info ; sales-exec.com
ASN/IP	168.245.19.130 / AS11377
Header Tags	X-SG-EID ; X-SG-ID
Pattern Match	Yes

Interpretation:
All indicators align with SendGrid’s email marketing infrastructure.

<img width="763" height="415" alt="image" src="https://github.com/user-attachments/assets/eef55158-01d3-41f9-9ecd-8eace5d124b0" />



## 1.5 Protocol Interpretation
Field	Value
Protocol	HTTP (SendGrid API) / SMTP (sales-exec.com)

Interpretation:
Marketing campaign sent via API → automated, not manually crafted.

<img width="820" height="159" alt="image" src="https://github.com/user-attachments/assets/6f87505b-584b-42f4-956c-103dc46a7b45" />

<img width="945" height="148" alt="image" src="https://github.com/user-attachments/assets/1b93fe91-2169-4ec1-8906-83e5a46abb1d" />



## 1.6 Email Authentication (SPF / DKIM / DMARC)
Mechanism	Result	Domain	Alignment
SPF	Pass	em4053.sales-exec.com	✔ Aligned
DKIM	Pass	sendgrid.info / sales-exec.com	✔ Aligned
DMARC	Pass	p=none	⚠ Not aligned (monitor mode)

Interpretation:
Normal authentication results for an ESP-sent marketing email.

<img width="798" height="201" alt="email-01-authentication-results" src="https://github.com/user-attachments/assets/8b91be24-3f45-4647-ad65-9ac692ad81f8" />




## URL & DOMAIN IDENTITIES
2.1 Domain Identity Mapping
Field	Value
Return-Path	bounces+1366688-4b01-blackwellrbrt=aol.com@em4053.sales-exec.com

MAILFROM (SPF)	sales-exec.com
DKIM d=	sales-exec.com
Received-From Domain	o1.ptr7709.sales-exec.com
Final Identity Match	Yes


## Interpretation:
All domains align logically in the context of an ESP sending on behalf of a marketing customer.

<img width="1420" height="833" alt="image" src="https://github.com/user-attachments/assets/d3db3832-0b67-4d91-8510-fcf399c9ea9a" />

<img width="890" height="762" alt="image" src="https://github.com/user-attachments/assets/37fc4278-105f-406d-9b60-0d0c315dd4bc" />

<img width="908" height="743" alt="image" src="https://github.com/user-attachments/assets/b5e41ecc-f99c-493b-9a6e-4c5d49170552" />




## CONTENT ANALYSIS
Indicator	Observation
Urgency	None
Sensitive Data Request	None
Tone	Upbeat / marketing
Grammar	Correct
Brand Consistency	Matches TruGreen
Content Risk	Low


## Interpretation:
Content fully matches expected promotional messaging.


<img width="1489" height="605" alt="image" src="https://github.com/user-attachments/assets/0b1c8603-5dbf-4ae1-a225-790377d06e34" />


## THREAT CLASSIFICATION
Classification	Reason
Benign	All authentication aligned; content legitimate; IP/domain clean; reflects normal marketing behavior.



## FINAL DETERMINATION
Final Verdict	Supporting Evidence
Benign	SPF/DKIM/DMARC pass; SendGrid ownership confirmed; no malicious signals; content consistent with TruGreen.


<img width="975" height="590" alt="image" src="https://github.com/user-attachments/assets/d12d1f20-29ce-4a89-8885-5e7eaef0a2e8" />

<img width="926" height="635" alt="image" src="https://github.com/user-attachments/assets/1d09ccd3-17a0-4844-9fad-6d34e750b7dc" />

<img width="923" height="625" alt="image" src="https://github.com/user-attachments/assets/6f67e1d9-7ae6-4bba-b604-a95af2d698e2" />

<img width="975" height="320" alt="image" src="https://github.com/user-attachments/assets/4cc1ccc5-8ae4-4ae4-a485-6fc0e8001daf" />




## RECOMMENDED ACTION

Action: Add sender/domain to Safe List



## MACHINE LEARNING LABEL OUTPUT

→ Save separately as:
labels/email-01-label.md

Field	Value
Classification	Low Risk
Subtype	Marketing
Risk Level	Benign


## Key Indicators

No malware/credential harvest signals

SPF/DKIM/DMARC passed

SendGrid (Twilio) confirmed as ESP

IP reputation clean via  VirusTotal


## Authentication

SPF: Pass (Aligned)
DKIM: Pass (Aligned)
DMARC: Pass (p=none)


<img width="975" height="320" alt="image" src="https://github.com/user-attachments/assets/c931a5e6-002e-4dfa-b92b-72c35f73d236" />


## REFLECTION

What I learned:

How to read multi-hop “Received” chains

How ESPs like SendGrid structure authentication

Why benign marketing emails often resemble malicious ones

Importance of alignment between MAILFROM, DKIM, and sending IPs

