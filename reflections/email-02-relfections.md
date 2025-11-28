## Email-02 Analysis — Learning Reflection

This analysis gave me a clearer glimpse into what a malicious email can look like, as well as what a legitimate Gmail-sent email header normally contains. I was confused at first because the chain of hops looked inconsistent and all over the place. Through research, I learned that this behavior is completely normal for emails sent from a Gmail account, which uses multiple internal relay hops.

I also need to remember that while I’m doing deep technical header analysis, the body of the email still matters. The content alone gave away a major red flag: the sender claimed to be from a financial services department of a major entity, yet the email was sent from a Gmail account, which was confirmed by both the “Received” section and the domain listed in the full header. That mismatch should always be a signal.

Another key takeaway was how modern analysts use AI to support research and fill in knowledge gaps. I saw firsthand how AI can help clarify and expand on my findings, but also why it cannot replace real analysis. Tools like VirusTotal and WHOIS also have limitations. If an attacker uses a Gmail account, the IP address will simply resolve to Google, appear clean, and show no malicious reputation. I remembered reading a LinkedIn post explaining that VirusTotal cannot be the only tool used to determine malicious intent, and this analysis proved that point. Sometimes the malicious indicator is not the infrastructure, but how the infrastructure is being used.

Overall, this was a great exercise that helped tie together everything I’ve been learning. I also walked away with stronger clarity on how to read headers:

Each hop begins with “Received:”

Whatever comes after “from” indicates the server used in that hop

Analysis must always be performed from the bottom up

And importantly, lines starting with X-* do not represent hops:

X-Gm-*

X-Proton-*

X-Forwarded-*

X-Message-State

X-Google-*

X-MSMail-*

X-Originating-IP

or any header that begins with X-

These reminders will definitely help me analyze future emails more accurately and efficiently.
