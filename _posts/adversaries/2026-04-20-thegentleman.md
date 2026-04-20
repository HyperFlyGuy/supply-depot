---
title: "The Gentleman Infrastructure Hunt"
layout: post
categories: Adversaries
---

**As new information surfaces I will try to keep this profile up to date**

## Summary
"The Gentleman" is a newer RaaS group (formed about mid 2025), that gained rapid popularity as it has claimed over 300+ victims. They offer affiliates a wide portfolio of lockers that support most major OS platforms that are found in corporate environments. The group maintains an onion site where they publish stolen data, however negotiations are conducted through a P2P instant messaging protocol [TOX](https://tox.chat/about.html). The combination of typical RaaS capabilities with a growing base of affiliates has allowed this group to go from relatively obscure to a major player within the Ransomware ecosystem.

## Observations
This particular Threat Actor seems to be disproportionately target US based entities in not particular sector. UK and Germany are then the next most targeted countries. This is a noticable shift from previous reporting as historically they have targeted APAC region entities.
These actors combined a multi-platform binary with built in lateral movement and group policy based deployment to allow even semi-skilled affiliates to have success at the enterprise level. SystemBC and Cobalt Strike C2's have been observed as the means of C2 for this group, but their ecosystems seems to be rapidly expanding and we can expect to see variation  in their C2 support.

## Capabilities
- **Sophistication Level:** Medium/High
- **Custom Tooling:** Yes 
- **Zero-day Usage:** Unknown

## Tooling
 - SystemBC usage reported
 - SOCK5 proxy
 - Cobalt Strike Payloads

## Known TTPs

### Initial Access
- The initial access vector at this point in time seems to be relatively unknown. Most reporting around the group only specifies activity after the have established domain admin permissions on the domain controller. Previous reporting suggested some CVE's in use but it is not consistent across multiple sources.

### Enumeration
- Previous reporting mentioning AngryIPScanner, nmap, and other general network mapping tools being used to recon the network.
- Enumeration of local and domain users along with domain trusts and domain controllers
- Enumeration via wmic of active security products

### Execution
- SystemBC has been flagged as a proxy malware in use by affiliates. It is unclear if it is directly integrated into the ransomware ecosystem or a tool leveraged by a particular operator.
- Deployment of Ransomware via group policy
- Remote Powershell

### Persistence
- Powershell via a scheduled task to maintain persistence
- Anydesk installation as a backup
- Registry run key set 

### Command & Control
- Cobalt Strike Beacons
- SOCK5 proxies

# Potential Attributes, Behaviors, or Indicators

## Organizational Structure
We do know that the Gentleman to operate as a Ransomware as a Service which means they exhibit many of the same qualities. It is likely that there initial access is done via an IAB then handed off to affiliated for action on objectives. This would likely cause a deviation of TTPs across various orgs which could make detection difficult. 

## Target Industries
Targeted industries seem to be fairly widespread with no one industry being targeted more than others.

## Target Countries
- Current (April 2026), trends show more focus on US based entities. However, historically they targeted APAC organizations.

## Peers
- Rumors of an affiliation with Russia, but nothing concrete that we can say for sure

# Detection Opportunities
- Enabling of Remote Desktop via cmd
- Installation of Anydesk
- NLtest/net user and domain enumeration

# Observed IOC's

Note there are many more IOCs related to this group and I have included the articles I used as references. The below IOCs are some that I was able to cobble together by doing some OSINT infrastructure hunting.

## SSH Thumbprint Correlation

SSH Fingerprint SHA256: 27631876e1257f8d24a617ce9e425355c120f4c7ae6f5bbac03aedd7317c872e
45.86.230[.]112
45.86.230[.]178
194.213.18[.]194 (Lower confidence)
Others were observed but do not appear related currently

## VT/Shodan Domain Pivots
kautzer.stieglers[.]net
zhongshengshijia[.]com (Low Confidence)

## VT file Relations
tkja.exe | 992c951f4af57ca7cd8396f5ed69c2199fd6fd4ae5e93726da3e198e78bec0a5 (SystemBC)

# References
- https://research.checkpoint.com/2026/dfir-report-the-gentlemen/
- https://www.trendmicro.com/en_us/research/25/i/unmasking-the-gentlemen-ransomware.html
- https://fortiguard.fortinet.com/threat-actor/6387/the-gentlemen-ransomware
- https://www.group-ib.com/blog/hastalamuerte-gentlemen-raas-ttps/
