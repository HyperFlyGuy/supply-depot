---
title: "Hypothesis-Driven Hunting Template"
layout: post
categories: Threat-Hunting
---

## Overview

This template provides a structured approach to hypothesis-driven threat hunting closely following a PEAK methodology. This is just an example template and to be honest it would make a bad hunt. The purpose of this is to just show what I typically would include when creating a new hunt.

## Preparation

This phase is where the bulk of our research and topic selection occurs. In the Hypothesis statement section we will go over how a hypothesis can evolve until we arrive at a desired hunt topic.

### Hypothesis Statement

Here you will find how a hypothesis is typically refined until it meets its final form. Your initial topic is allowed to be broad, in fact for me it typically helps me come up with some creative hunt ideas that I may never have thought of previously.

`1st Form: Threat actors will establish persistence`

We decided that most Threat Actors that we are targeting will likely establish some sort of persistence in the compromised environment. However, there are hundreds of ways that this can be achieved we would need to conduct some research to narrow our scope and refine our hypothesis.

`2nd Form: Threat Actors will use Registry Run keys to establish persistence on endpoints across the environment`

This is a simple iteration but I think you get the idea. With more complex topics or less researched subjects you will need to revisit this hypothesis as you discover more information and execute your hunt. As you understand more and more about the available telemetry and what is expected in your environment you can tailor your hypothesis to properly evaluate threats that may be active within your organization.

## Execution
This part is a bit difficult to template out for you. In this section I typically like to have some sort of pseudo-code that describes the searches/queries you can use, if I am disseminating to the general public (I'm personally not a huge fan of sigma rules). As you will see with any of the hunts that you observe on this page. However, I do recommend that you keep queries here that match the systems that are in use within your organization. 

### Logic to gather all registry events that contain Run 

```
analysis_q = []
for endpoint in endpoints:
  if endpoint.registryevent contains "Run" or endpoint.registryevent contains "RunOnce":
    analysis.append(endpoint.registryevent)
```

## Actions

What actions do we need to take based off our data and analysis? Some things that you'll want to track could be:
- New detections or modifications to existing detections
- Hunt documentation or hunt report 
- Any identified gaps or risks
- Additional hunt ideas as a result of this hunt.

## Knowledge

This section will contain all the knowledge that you should keep a record of for future hunters. This can be any issues with the data that you came across, false positives that you may have observed, any other nuances that you believe would be beneficial if another hunter were to rerun this hunt
