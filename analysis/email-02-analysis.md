# Basic Metadata 

---

### **Fields to Capture**

- **Sender Name:** John Lee  
- **Sender Email Address:** sandraleejohn591@gmail.com  
- **Subject Line:** “Reference number: SFSA/UP2950/8PUK”  
- **Date Received:** 11/19/2025  
- **Email Provider:** Gmail  
- **Email Folder Source:** Spam  


<img width="893" height="69" alt="email-02-bottom-received" src="https://github.com/user-attachments/assets/ccdeeb1e-50fb-4c95-8775-fef5791eadb1" />



## Initial Risk Assessment

- **Does the email try to get me to click a link, open an attachment, or sign in?**  
  No. There were *no links, attachments, or sign-in prompts* in the email body.

- **Does the sender seem unusual or unknown?**  
  Yes. The sender is unknown, and the content appears unusual because it references **“UN accounts,”** which is atypical for legitimate communication.

- **Is there urgency, threats, money claims, or account warnings?**  
  Yes. The email contains **money-related claims**, including:  
  *“The auditor report shows that you have been going through hard times by paying a lot of money to certain groups of individuals for the transfer of funds to your bank account.”*

- **Does the branding appear suspicious?**  
  Yes. The email does **not** appear to come from any recognized organization, company, or marketing source.

---

## Full Email Body Review  

<img width="649" height="709" alt="email-02-email-body" src="https://github.com/user-attachments/assets/ef057a0f-a4bd-44e3-b6e5-d489bf801cf4" />


### Red Flags Identified in the Email Body

#### **Urgency (Pressure to Act Quickly)**
The email does not explicitly state an urgent deadline, but urgency is strongly *implied* through the tone and wording:
- *“We therefore advice you stop further communication with any correspondence outside this office…”*  
- *“…your payment file was forwarded to our office for the immediate transfer of US$2,550,000.00 to your bank account…”*  
These statements attempt to create emotional pressure, restrict outside communication, and push the recipient toward compliance.

#### **Authority Abuse (Pretending to Be an Official Entity)**
The sender claims to represent a **Financial Services Department in the UK**, a tactic commonly used in advance-fee fraud and government-themed scams.

#### **Grammar & Language Red Flags**
The email contains numerous linguistic errors typical of phishing emails:

### **Missing Words / Articles**
- *“after thorough review”* → missing **a**  
- *“to UN accounts”* → missing **the**

### **Capitalization Errors**
- “Inheritance” randomly capitalized  
- “funds,etc.” missing space and improper capitalization  
- “keldford” appears multiple times uncapitalized  
- “Full Names” and “Telephone” capitalized mid-sentence  
- “financial services, UK” incorrectly formatted

### **Punctuation / Spacing Errors**
- *“funds,etc.”* → should be **“funds, etc.”**  
- Multiple comma splices  
- Missing spaces after punctuation

### **Incorrect Word Choice / Wrong Forms**
- *“auditor reports”* → incorrect form (should be **auditor’s reports**)  
- *“a compensation”* → incorrect; “compensation” is uncountable  
- *“funds retarded”* → incorrect word choice and meaning  
- *“We therefore advice”* → wrong form (“advice” vs. “advise”)  
- *“met up with the whole funds transfer requirements”* → wrong phrasal verb and unnatural phrasing  
- *“stop further communication with any correspondence”* → incorrect use of “correspondence”

### **Subject–Verb Agreement Errors**
- *“all which has been delayed”* → should be **“all of which have been delayed”**

### **Sentence Structure Issues**
- Awkward or incorrect phrasing such as  
  *“a compensation for your funds retarded”*  
- Run-on sentences and unclear clause connections

### **Formatting / Style Issues**
- *“with the below information”* → should be **“with the information below”**  
- *“All correspondences”* → uncommon plural; “correspondence” is typically a mass noun

#### **Branding Inconsistencies**
No legitimate organization branding, formatting, or structure is present. Email uses plain text with no professional identifiers.

#### **Suspicious Links**
The email contains **no links**, but this is not unusual for scam types that rely on replies instead of clicks.

#### **Unusual Requests**
The email sets up a scenario involving:
- Money claims  
- Government involvement  
- Account transfers  
- An implied instruction to reply with personal information  

This is consistent with **advance-fee fraud** and **419 scam patterns**.

---

### **Notes**
- The message uses emotionally manipulative wording regarding hardship and funds.  
- Claims of government involvement without evidence.  
- Multiple grammar and structural issues typical of mass scam emails.  
- No clear reason for contacting the recipient.  
- Mentions large sums of money ($2.55M), a hallmark of advance-fee scams.

---

## Extract Full Email Headers  

<img width="828" height="832" alt="email-02-header-full" src="https://github.com/user-attachments/assets/ac6a66a1-8679-4c7c-a940-441528bf9b50" />

## Authentication Results Overview (SPF / DKIM / DMARC)

--

<img width="880" height="202" alt="email-02-authentication results" src="https://github.com/user-attachments/assets/6d2eb9ba-9613-4e78-a788-0dd1b0987820" />


---

# Authentication Findings

| Mechanism | Result | Domain | Alignment | Interpretation |
|-----------|--------|---------|-----------|----------------|
| **SPF** | PASS | gmail.com | ❌ Not aligned | SPF passed because Gmail IP is authorized for gmail.com. However, the MAILFROM domain does NOT match the From: domain — red flag. |
| **DKIM** | PASS | gmail.com | ❌ Not aligned | DKIM was signed by gmail.com, but the displayed From address **does not belong to the sender’s claimed identity**. Red flag: signing domain is generic. |
| **DMARC** | PASS (p=none) | gmail.com | ❌ Not aligned | DMARC passes because Gmail’s domain authenticates itself — but alignment still fails. This means **Gmail authenticated Gmail**, not the sender’s identity. |

---

## Interpretation 

### **SPF Pass — but NOT a sign of legitimacy**
- Gmail allows its servers to send mail for gmail.com  
- But this email claims to be a “Financial Services, UK” entity  
- That identity **IS NOT** tied to gmail.com  
- Therefore SPF → **meaningless here**  

**Red Flag:** Attackers often use free email providers so SPF passes even during fraud.

<img width="780" height="124" alt="email-02-spf results" src="https://github.com/user-attachments/assets/64efb522-9385-43c2-a96e-6b568ed77713" />

---

### **DKIM Pass — but signed by Gmail, not the claimed sender**
- DKIM signature is valid  
- But signed by **gmail.com**, not by any financial institution domain  
- Message was not altered — but:
  - Sender identity is **not validated**
  - Anyone can create a Gmail account and sign mail with Gmail’s DKIM

**Red Flag:** DKIM pass ≠ proof of legitimacy when the domain is generic.

<img width="504" height="142" alt="email-02-dkim signature results" src="https://github.com/user-attachments/assets/bff40adf-e398-460b-a3b6-b77619c3fd97" />

---

### **DMARC Pass — but only because Gmail authenticated itself**
- DMARC passes under **p=none**, which requires no enforcement  
- Alignment fails because:
  - From: is not a financial institution  
  - MAILFROM: gmail.com  
  - DKIM: gmail.com  

So DMARC passes technically **but confirms NOTHING about legitimacy**.


**Red Flag:** DMARC “pass” with misalignment is one of the most common phishing indicators.

<img width="726" height="123" alt="email-02-dmarc results" src="https://github.com/user-attachments/assets/e2e8f53f-5cb2-49f4-a936-1a221ccec8da" />

---

# Full Header Forensics (Domain Chain Analysis)

## Interpretation

Does the sending chain make sense?	Yes — Gmail’s internal hop sequence is normal.

Any suspicious jump from unrelated server?	Suspicious sender identity, not the hops.

Red flags:
• Gmail account impersonating a UK financial authority
• No official organizational domain
• No DKIM alignment for any UK gov/finance domain
• Body content matches common scam patterns

Is the Received: order inconsistent?	No — Gmail hops appear in the correct internal order.
Does the source IP belong to the claimed domain?	Yes — It belongs to Gmail, not the impersonated UK authority.

### Notes About Gmail’s Internal Hops

Gmail uses multiple relay layers during message processing:

IPv6 handoff

Google Frontend (internal routing)

Google Mail Transfer Agent (MTA)

Anti-spam and anti-abuse scanning

Internal routers and delivery relays

These will ALWAYS appear and are not indicators of malicious behavior.

Overall Forensic Verdict

Header chain is legitimate Gmail infrastructure.
The sender identity is fraudulent — not the email route.

# VirusTotal Reputation Checks

<img width="688" height="404" alt="email-02-virustotal-ip" src="https://github.com/user-attachments/assets/bf84febe-e73f-4588-8884-0c620a23ae4b" />

## Interpretation

No security vendors flagged this URL as malicious.
-	VT clean does not change the risk
-	Gmail infrastructure cannot be used to validate legitimacy
-	Gmail is frequently used by scammers for free

# WHOIS / Domain Age Analysis

## Interpretation

First thing I notice when utilizing domaintools was that the listed ASN was not identified in the header per my analysis.  But this is normal given Gmail hides ASN inside internal routing and IPv6 handoffs, so the ASN will not be directly exposed.  Gmail’s ASN is AS15169.  I must note again that the suspicious comes from the following fact:

-	Financial authority claim 
-	Sender uses Gmail 
-	Not an official gov.uk domain 

•	Domain creation date: Mar 30, 2000 
•	Registrar: Google LLC 
•	Country / privacy info: US 
•	Suspicious patterns: none 


# Link & Attachment Analysis: No links were provided in this email 

# Final Verdict

This email is clearly malicious.

## Indicators include:
•	Mismatched identity (claiming UK financial authority but sent via Gmail)
•	DKIM alignment fails
•	DMARC fails due to alignment
•	Numerous grammatical and structural red flags
•	The sender email and content strongly resemble known advance-fee fraud scams


