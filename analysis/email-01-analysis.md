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


## DKIM Analysis 

**DKIM #1**
**Result**: Pass

**Domain**:d=sales-exec.com

**Selector**: s=s1

**DKIM Signature Extracted**:
v=1; a=rsa-sha256; c=relaxed/relaxed; d=sales-exec.com; h=content-transfer-encoding:content-type:date:from:mime-version:subject: reply-to:sender:to:list-unsubscribe:list-unsubscribe-post:cc:content-type:date: from:subject:to; s=s1; bh=INgY3Y7ALRevXREI42fGze/nQiPZbk8VK3BXScXpYaU=; b=Bb4lSbLTGsm5bPSB8V08nRh4XXtCvmca/KhR5XRcJgNdzv0ElLxKY9cu2wi8P346VWiE WR8DXqxUSpe6rQJQSFWScSw3ZWjBg4ZVKTHJy1djsMSDmeoVuEclzaa3ExeGNEPNI8CNXJ evHQkiT/S9WRg2q3796FLaBni+b8yPT8y11CGn3BBnnsELyoHCSvSjTtR70+FECs9vZU+a /coomjh1vCf7Gms3a8TNzPADAzIpfrTQLsvJRE+4Wve/0fQNy1wo76/JFkXwUGeI26jh7F 8FJGxjP+hNCR45VhsB4HUqlvuwdeyZ2ZTyKpztakArux4q8suoypQ9TRbcO9wGsA==

**DKIM Public Key Record Extracted**:
k=rsa; t=s; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqmXlq2KC7B/56KFrfPLXHuMPfEy6i4ll0/SloT7X11P9iVKxEiZ2sBKFPolgxhci760dKWADDjir2NPrY5bLQN0ynYsKAtVBWbTj45Wv7BqXaHdpif/NCRVdHpi3rkHcl0jGMjzvaR517L7SsUZMWQaVcipcCrE9wPBGrUcLb1dbjwoWEKce8Gy1EiwM+FtmqgDnEn+rbt/m2lZdUdh4DNaEJGaPelqZH8uANWgZ6vdRm8hZ11kIJy2TZTvHZSLNaKwtF3OkeTZ1YIk1LejKH0Z3seVHqNH1qcbf0tQFLrLf0/vhVB49R2rECEzHk7IgJisBUbJQLZ+OAflr8oLsrQIDAQAB

**Signature Validation**:
- Valid -crytographic check passed

**Alignment Check**:
- Aligned
- DKIM d=sales-exec.com  matches the Header-From domain sales-exec.com

**Key Length**: 2048
- Acceptable

**Selector Configuration Health**:
- Public Key Present in DNS: Yes 
- Selector uses appropriate TTL: Yes
- Valid DKIM version (v=DKIM1): Yes 

**Red flags/Notes**: None 

