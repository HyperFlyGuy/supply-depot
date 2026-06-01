---
title: "Business Email Compromise: Rule Creation Hunt"
layout: post
categories: Threat-Hunting
---

## Overview

Kali365 is a cloud-based phishing as a service platform that provides advanced phishingcapabilities to Threat Actors of all levels. Kali365 operates under an affiliate program that allows partners to pay a monthly fee to access the platform. Once a partner is onboarded, they can access the platform and use advanced phishing features to target organizations. These capabilities include:
- AI assisted lure generation
- Reverse proxy credential harvesting
- Session token hijacking
- Device Code mode
- Cookie Link mode
These are some of the more unique capabilities of Kali365 that make it a powerful phishing platform for Threat Actors. 


## Preparation

The focus of this hunt is to track and note any infrastructure that may be used by Kali365 for phishing. Typically, Kali365 infrastructure leaves four (4) ports open for communication
- 22: OpenSSH
- 80: HTTP nginx
- 443: HTTPS nginx (Victim Facing phishing portal)
- 8443: HTTPS nginx with custom port (Panel access)

Using an initial node from a [recent blog] (https://www.todyl.com/blog/kali365-phaas-inside-attack-infrastructure) we were able to pivot and attempt to identify additional infrastructure nodes. 

## Execution
We started by investigating the `66.179.30[.]87` node via shodan to see if there was any additional information in the banners or headers that we could use to pivot. I want to say that the opsec on this node was particularly bad as the HTML title was `K365 Control`.

We noted from multiple articles that the administrator panel is typically served on port 8443. Using this information we took the html hash and searched across shodan.

**Shodan Search**
```
`http.html_hash:105613739`
```

This search left us with five (5) total results and three (3) unique IP addresses. We then took the IP addresses and searched for any additional information in the shodan database, but found nothing of interest. We did note four (4) unique domains associated with the IP addresses that were flagged on Virustotal as being associtated with the K365 phishing kit.

## Actions
- **Block Device Code Authentication** using Conditional Access (CA) policies where not explicitly required and closely audit any exceptions.

## Knowledge

### IOC's 

```
Domains:
boss.securehubcloud[.]com
duemineral[.]uk
blackoctopusking[.]live
blackoctopusking[.]xyz

IP:
66.179.30[.]87
64.7.198[.]96
72.5.42[.]76
```

## References 
https://www.ic3.gov/PSA/2026/PSA260521
https://arcticwolf.com/resources/blog/token-bingo-dont-let-your-code-be-the-winner/
https://windowsforum.com/threads/kali365-device-code-phishing-how-it-bypasses-mfa-in-microsoft-365.421119/
https://www.todyl.com/blog/kali365-phaas-inside-attack-infrastructure
