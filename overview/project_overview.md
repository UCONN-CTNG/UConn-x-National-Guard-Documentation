---
layout: default
title: "Project Overview & Requirements"
permalink: /project_overview/
date: 2020-12-09
---
# Project Overview
# Connecticut National Guard Cyber Range 


## Background:
The Connecticut National Guard (CTNG) Cyber Range is a cloud-hosted cyber range to facilitate training for its personnel and partners. In this environment, the CTNG must be able to create a scenario to faithfully replicate either a critical infrastructure or local municipality’s network and provide either hosted or remote-connected adversaries. (i.e. the CTNG provides the threat, Red Team, or facilitates bringing a Red Team via remotely connected systems). The range must provide a realistic set of threats, vulnerabilities and exploits that mimic real-world attacks and provides a means for “blue team” systems to be added to the network, post exploitation, simulating a cyber incident response. The end state is a well-orchestrated storyline that ties into a realistic set of attacks that mimic threats from script kiddy, Low Level hackers through advanced persistent threat and nation-state actors.

## Project Requirements:
- Design training excercises that simulate common attacks/scenarios that memebers of the National Guard cybersecurity team may run into. (Sample scenarios are Ransomware, Phising, Web Defacement, Malvertising, etc.)
- Provide documentaion on how to create and setup training scenarios for future use

## Dependecies:
The cyberrange has been setup on hardware belonging to the CTNG. The vCenter instance that houses the cyberrange already contains various different servers and virtual machine instances, but the team is free to create and use their own instances. This vCenter instance can be accessed through a jump server after connecting through a Meraki VPN with the provided credentials. The cyberrange, all hardware, the VPN, and the jump server are all owned, adminstratively controlled, and maintained by the CTNG. 

[Main Menu](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation)
