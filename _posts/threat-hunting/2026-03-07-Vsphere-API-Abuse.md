---
title: "Cloud Session Hijacking"
layout: post
categories: Threat-Hunting
---

## Overview

Observed in Muddled Libra (Scattered Spider) September 2025 incident. Attackers provisioned a VM named "New Virtual Machine" via vSphere within 2 hours of initial access, then used it for 15+ hours as their primary operations host — no EDR coverage.

Why This Hunt?
VMs provisioned by attackers won't have EDR/XDR agents deployed, giving them a completely unmonitored host to run tools, dump credentials, and stage exfiltration from
vCenter audit logs capture VM lifecycle events including creation tasks — hunting for VMs created by unexpected users, outside change management windows, or with generic default names can surface rogue infrastructure before lateral movement begins
Once a rogue VM exists in the environment, attackers can mount virtual disks (VMDKs) of other VMs, including powered-down domain controllers, to extract sensitive files like NTDS.dit without generating any endpoint telemetry on the target
Organizations with broad vCenter permissions or self-service provisioning are at higher risk, as malicious VM creation may blend in with legitimate activity


## Preparation



### Hypothesis Statement


## Execution

## Actions

## Knowledge
