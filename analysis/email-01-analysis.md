## SPF Analysis

**Result**: Pass

**Domain** (Envelope From/Return-Path): sales-exec.com

**Record Extracted**:
v=spf1 ip4:167.89.7.21 ip4:168.245.19.130 -all

**Observed Sending IP**: 168.245.19.130

**Sending IP Authorized?**  
Yes — the sending IP 168.245.19.130 appears in the SPF record and is authorized to send mail for sales-exec.com.

****Alignment***:
Aligned — the Return-Path domain matches the domain used in SPF authentication.

**Red Flags / Notes**: None detected
- SPF record is valid and syntactically correct: Yes  
- Suspicious mechanisms (`+all`, `?all`, unusual includes): No  
- Sending IP belongs to approved ESP pool: Yes  
- Authentication matches actual sending path: Yes  


## DMARC Analysis
**Results**: Failed 

**Domain(Header From)**: sales-exec.com

**DMARC Record Extracted**: 
v=DMARC1; p=none; sp=none; adkim=r; aspf=r; rua=mailto:dmarc_agg@vali.email,mailto:dmarc-reports@sales-exec.com; ruf=mailto:dmarc-failures@sales-exec.com; fo=1

**DMARC Policy Applied**: DMARC Quarantine/Reject Polocy not enabled

**Alignment Check**: Aligned; The DMARC alignment check succeeds because the Header-From domain matches.

**Identifier Alignment**:
- SPF Indentifier Aligned: Yes
- DKIM Identifier Aligned: Yes

**Sending Domain Authenticated**: Yes 

**Forensic/Failure Reporting Addresses**: 
- ruf: malito:dmarc-failures@sales-exec.com
- rua: malito:dmarc_agg@vali.email,malito:dmarc-reports@sales-exec.com

**Red Flags/Notes**:
- DMAR Record syntax valid: Yes
- Policy Protective: No (Policy is None)
- Alignment Mode: Relaxed
- External reporting used: Yes 


