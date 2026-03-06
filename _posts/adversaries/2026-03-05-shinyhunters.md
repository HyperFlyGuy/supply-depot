---
title: "ShinyHunters Adversary Analysis"
layout: post
categories: Adversaries
---

# ShinyHunters Analysis

## Overview:

ShinyHunters (also known as ShinyCorp) is an international, financially-motivated cyber threat group that first emerged in 2020, quickly gaining notoriety for orchestrating high-profile data breaches and extortion campaigns against major global brands (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Who is ShinyHunters?", Lines 34-41). Despite the playful, Pokémon-inspired name suggesting a community of harmless enthusiasts, ShinyHunters has become deeply entrenched in cybercrime, specializing in the theft and sale of vast databases on dark web forums (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Who is ShinyHunters?", Lines 38-52).

The group has claimed responsibility for multiple significant cyberattacks, leaking personal information of over a billion internet users through high-profile breaches of companies such as Tokopedia (91 million users), Microsoft GitHub (500GB of data), Wattpad (271 million users), and AT&T (70+ million records) (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters' High-Profile Attacks", Lines 162-312). ShinyHunters has also established dominance in the dark web's cybercriminal landscape by taking ownership of BreachForums, one of the most frequented hacker forums, following the FBI seizure of RaidForums (Source: Dark Web Profile_ ShinyHunters.txt, Section: "The Current Owners of One of the Most Popular Cybercriminal Forums", Lines 447-483).

After a period of relative inactivity following the arrests of four members in mid-2024, ShinyHunters resurfaced in 2025 with a new wave of sophisticated attacks targeting Salesforce CRM systems at high-profile companies including Qantas, Adidas, LVMH, Louis Vuitton, Google, and Allianz Life (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Key Points", Lines 12-26; Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 497-550). These recent campaigns demonstrate a significant evolution in tactics, incorporating sophisticated voice phishing (vishing), credential harvesting, and SaaS data exfiltration techniques that closely mirror tactics used by the Scattered Spider collective (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Introduction", Lines 14-46).

## Observations:

- ShinyHunters operates as a financially-motivated group specializing in data-theft extortion, using underground forums like BreachForums to monetize stolen data through sales or ransom demands (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Who is ShinyHunters?", Lines 34-52).

- The group appears to operate as a flexible extortion-as-a-service model with potential overlap with other threat groups such as Scattered Spider and possibly former members of Lapsus$ (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 531-538).

- Google Threat Intelligence Group tracks ShinyHunters-related activity under multiple threat clusters (UNC6661, UNC6671, UNC6240), suggesting multiple individuals or partnerships may be involved in operations (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Introduction", Lines 32-46).

- Evidence suggests collaboration or overlap with Scattered Spider, including a BreachForums user with alias "Sp1d3rhunters" (combining both group names) who claimed "the two groups are the same and have always been the same" (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Claims of Collaboration in Interviews and Forum Activity", Lines 101-111).

- The group has demonstrated ability to conduct simultaneous multi-sector campaigns targeting retail trade (April-May 2025), insurance (June-July), and aviation (June-August) (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Simultaneous Campaigns Across Sectors", Lines 113-124).

## Capabilities:

ShinyHunters demonstrates sophisticated capabilities across the full attack lifecycle, from initial access through data exfiltration and extortion. Their operations primarily leverage social engineering, credential theft, and cloud/SaaS exploitation to achieve financially-motivated objectives.

**Initial Access and Credential Theft:**
- Vishing/Phishing - T1566: Phishing, T1598: Phishing for Information, T1078.002: Valid Accounts: Domain Accounts, T1078.004: Valid Accounts: Cloud Accounts (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 551-598)
- GitHub Repository Exploitation - T1213: Data from Information Repositories (Source: Dark Web Profile_ ShinyHunters.txt, Section: "How Does ShinyHunters Hack?", Lines 84-106)

**Cloud and SaaS Exploitation:**
- Cloud Infrastructure Discovery - T1580: Cloud Infrastructure Discovery (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 576-577)
- Unsecured Cloud Bucket Exploitation - T1530: Data from Cloud Storage Object (Source: Dark Web Profile_ ShinyHunters.txt, Section: "How Does ShinyHunters Hack?", Lines 93-98)
- Steal Application Access Tokens - T1528: Steal Application Access Token (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 574-575)

**Lateral Movement and Collection:**
- Software Deployment Tools - T1072: Software Deployment Tools, T1210: Exploitation of Remote Services (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 578-582)
- Data Collection from SaaS - T1213: Data from Information Repositories, T1530: Data from Cloud Storage Object (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 592-596)

**Exfiltration:**
- Exfiltration Over Web Service - T1567: Exfiltration Over Web Service (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters TTPs – MITRE ATT&CK Framework", Lines 597-598)

## Tooling:

- **Victim-Branded Credential Harvesting Sites** - Custom phishing pages designed to impersonate legitimate corporate SSO portals. Domains commonly follow patterns like `<companyname>sso.com`, `<companyname>internal.com`, `<companyname>okta.com`, or `ticket-<companyname>.com`. These pages capture SSO credentials and MFA codes during vishing attacks (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 65-82; Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Infrastructure Connection", Lines 131-175).

- **Malicious OAuth Connected Apps** - Apps disguised as legitimate tools (often masquerading as "My Ticket Portal" or "Ticket Dashboard") that trick employees into authorizing access, allowing attackers to steal Salesforce and other SaaS data at scale (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "ShinyHunters Adopts Scattered Spider's Signature Moves", Lines 86-98; Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 503-506).

- **ToogleBox Recall** - A Google Workspace add-on used to search for and permanently delete emails, specifically used to delete "Security method enrolled" notifications from Okta to hide MFA device registration from victims (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 203-231).

- **PowerShell for SaaS Data Exfiltration** - PowerShell scripts used to download sensitive data from SharePoint and OneDrive at scale (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Similar Activity Conducted by UNC6671", Lines 281-283).

- **Mullvad VPN and Residential Proxies** - VPN services and residential proxy networks (including Mullvad, Oxylabs, NetNut, 9Proxy, Infatica, nsocks) used to obfuscate data exfiltration and hide attacker origin (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "ShinyHunters Adopts Scattered Spider's Signature Moves", Lines 97-98; Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Network Indicators", Lines 359-369).

- **Limewire for Data Hosting** - File hosting service used to host samples of stolen data as proof in extortion demands (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 243-254).

- **ShinyHunters Data Leak Site (DLS)** - A dedicated leak site named "SHINYHUNTERS" that emerged in late January 2026 listing alleged victims, with contact information (shinycorp@tutanota.com, shinygroup@onionmail.com) (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 258-265).

## Potential Attributes, Behaviors, or Indicators:

### Organizational Structure:

ShinyHunters appears to operate as a loosely affiliated collective rather than a hierarchical organization. Key structural observations include:

- The group likely operates as a flexible "extortion-as-a-service" model (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 531-532)
- Multiple individuals appear involved, as evidenced by continued operations despite the June 2024 arrest of a key operator who transferred control of BreachForums to IntelBroker (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 525-530)
- Google Threat Intelligence tracks activity under multiple clusters (UNC6661, UNC6671, UNC6240), suggesting distinct individuals or partnerships (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Introduction", Lines 32-36)
- The group has maintained relationships with forum administrators including "Pompompurin" (arrested former BreachForums moderator) and "Baphomet" (Source: Dark Web Profile_ ShinyHunters.txt, Section: "The Current Owners of One of the Most Popular Cybercriminal Forums", Lines 454-468)

### Target Industries:

- **SaaS/Cloud Platforms**: Salesforce CRM, Okta, Microsoft SharePoint, OneDrive, Google Workspace, Slack (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "Introduction", Lines 27-31)
- **E-commerce**: Tokopedia, Bhinneka (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Claimed Breach of Tokopedia", Lines 175-192)
- **Retail Trade**: Pizza Hut Australia, Nike, Adidas, LVMH, Louis Vuitton, Dior, Audemars Piguet (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters' Alleged Attack on Pizza Hut Australia", Lines 250-279; Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Similar Domain Formats", Lines 135-146)
- **Technology**: Microsoft, GitHub, Pixlr, Snowflake (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters' Supposed Infiltration of Microsoft GitHub", Lines 193-215)
- **Telecommunications**: AT&T (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Leak Over 70 Million Records Allegedly Stolen from AT&T", Lines 280-312)
- **Financial Services**: Banks, insurance companies - increased targeting since July 2025 (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Targeting Shifts from PSTS to Finance", Lines 195-211)
- **Aviation**: Qantas (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks", Lines 497-499)
- **Insurance**: Allianz Life (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks", Lines 499-501)
- **Entertainment/Media**: Wattpad, Ticketmaster (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Alleged Sale and Leak of Wattpad User Data", Lines 216-230)

### Target Countries:

- **Primary**: United States (67% of all ransomware leak site victims are US companies; majority of impersonating domains target US organizations) (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "US Continues to Top Impersonating Domain Creation Tables", Lines 217-230)
- **Secondary**: United Kingdom, France, Australia (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "US Continues to Top Impersonating Domain Creation Tables", Lines 218-219)
- **Historical targets**: Indonesia (Tokopedia), Europe (financial organization) (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Claimed Breach of Tokopedia", Lines 186-192; Source: ShinyHunters_ An Insight into Future Extortion Tactics_ _ ZeroFox.txt, Section: "Details", Lines 174-175)

### Observable Attack Patterns:

1. **Vishing-led Initial Access**: Attackers impersonate IT support staff, calling employees claiming to update MFA settings, then directing them to credential harvesting sites (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 67-74)

2. **MFA Bypass via Social Engineering**: After capturing SSO credentials and MFA codes, attackers register their own device for MFA (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 72-75)

3. **Evidence Destruction**: Deletion of security notification emails using ToogleBox Recall to hide MFA device enrollment (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 203-211)

4. **Targeted SaaS Data Searches**: Searching cloud applications for documents containing keywords like "poc," "confidential," "internal," "proposal," "salesforce," "vpn" and targeting PII in Salesforce (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 104-110)

5. **72-Hour Extortion Deadline**: Ransom notes specify payment amount, BTC address, and threaten consequences if not paid within 72 hours (Source: Tracking the Expansion of ShinyHunters-Branded SaaS Data Theft _ Google Cloud Blog.txt, Section: "UNC6661 Vishing and Credential Theft Activity", Lines 244-252)

## Peers:

- **Scattered Spider** (aka The Com) - Strong evidence of collaboration or overlap, including shared tactics (vishing, Okta phishing pages, domain registration patterns) and a BreachForums user "Sp1d3rhunters" claiming the groups "are the same" (Source: ShinyHunters Targets Salesforce Amid Clues of Scattered Spider Collaboration.txt, Section: "Are ShinyHunters and Scattered Spider Joining Forces?", Lines 83-124)
- **Lapsus$** - Possible overlap with former members (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 534-535)
- **GnosticPlayer** - Similar operational pattern of mass data dumps (Source: Dark Web Profile_ ShinyHunters.txt, Section: "Who is ShinyHunters?", Lines 57-59)
- **Clop** - Similar extortion tactics: targeting cloud platforms with downstream customers, omitting encryption payloads, using data theft and public pressure for extortion (Source: ShinyHunters_ An Insight into Future Extortion Tactics_ _ ZeroFox.txt, Section: "Parallels with Clop's 2023 Extortion Activity", Lines 108-156)

## Known Members/Affiliates:

- **Sebastien Raoult (aka "Sezyo Kaizen")** - 22-year-old French citizen sentenced to 3 years in prison and $5 million restitution. Created deceptive web pages for phishing schemes to harvest user credentials (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Hacker Sezyo Kaizen Sentenced to Prison", Lines 417-446)
- **Pompompurin** - Former BreachForums moderator, arrested by law enforcement (Source: Dark Web Profile_ ShinyHunters.txt, Section: "The Current Owners of One of the Most Popular Cybercriminal Forums", Lines 454-468)
- **Baphomet** - Administrator alongside Pompompurin, seized by law enforcement in May 2024 BreachForums disruption (Source: Dark Web Profile_ ShinyHunters.txt, Section: "The Current Owners of One of the Most Popular Cybercriminal Forums", Lines 467-468; Source: ShinyHunters_ An Insight into Future Extortion Tactics_ _ ZeroFox.txt, Section: "BreachForums Disruption", Lines 200-211)
- **IntelBroker** - Received transfer of BreachForums control from arrested operator in June 2024 (Source: Dark Web Profile_ ShinyHunters.txt, Section: "ShinyHunters Behind CRM Attacks on Qantas, Adidas, and Others", Lines 526-528)

# References

- https://socradar.io/blog/dark-web-profile-shinyhunters/
- https://reliaquest.com/blog/threat-spotlight-shinyhunters-data-breach-targets-salesforce-amid-scattered-spider-collaboration/
- https://www.zerofox.com/intelligence/shinyhunters-an-insight-into-future-extortion-tactics/
- https://cloud.google.com/blog/topics/threat-intelligence/expansion-shinyhunters-saas-data-theft
