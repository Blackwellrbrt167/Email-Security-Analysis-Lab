## Email-01 Analysis — Learning Reflection

This analysis took time because I wanted to approach it the same way an analyst would—carefully, methodically, and with a genuine understanding of what each component meant. I can honestly say this was the beginning of my deep study into email security and authentication.

Once I understood the workflow and how each section connected, I started moving much faster through the analysis.

One of the biggest challenges was locating the information within the header. I went line-by-line to find each data point. Even though MXToolbox summarized everything for me, I still wanted to build the stamina and skill of identifying these elements directly in the raw header. Because this email used an ESP, I kept getting confused by the presence of two DKIM signatures. At first, this threw me off, but eventually I understood that this is normal when an ESP is involved.

Patterns I Noticed

When a company uses an ESP, there will almost always be two DKIM signatures—one from the corporate domain and one from the ESP. Also, while the general rule of thumb is that the bottom-most “Received” header shows the originating server, an ESP changes that pattern. With ESP-based emails, the bottom-most entry reflects the ESP itself. To identify the true sender, I must follow the received chain and verify the associated IP ownership.

As I continue analyzing more emails, I expect to become more efficient. This first one required a lot of digging, note-taking, and verifying where each item was found, but now many of those gaps are filled. The concepts make much more sense, and the process is becoming more natural.
