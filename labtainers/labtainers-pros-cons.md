---
layout: default
title: "Labtainers Pros vs Cons"
permalink: /labtainers/pros-cons/
date: 2020-11-22
author: Chris
---

# Labtainers pros and cons

After the first meeting with the Connecticut National Guard, it became apparent that they wanted the UConn team to develop a series of test scenarios, where the student would be able to observe (and learn to defend against) various cybersecurity attacks.

There are various approaches to create such scenarios, one of which is to develop new environments for the labtainers software, and another of which is to develop and deploy scenarios for VMWare machines.

After some testing and deliberation, it became apparent that labtainers software may be useful to the Connecticut National Guard for situations already contained in the labtainer suite (i.e. more commonplace scenarios, such as learning about nmap and DNS spoofing).

For more specific scenarios which are not included by the labtainer suite, the team has decided to implement these scenarios in VMWare (e.g. ransomware, defacement scenarios which do not already exist in labtainers).

### Pros of using labtainers
- Suite of containers already ready to deploy
- Easy for users/students to install
- Each lab can be parametrized, so that certain data is random each time the lab is run.
- Scenarios can be built to be automatically graded
- Examples of other labtainers are freely accessible (makes development easier)
- Creating new scenarios is relatively easy
- Once a new scenario is created, it can be shared to the labtainer community

### Cons of using labtainers
- Scenarios that the Connecticut National Guard requested are not currently in the labtainer suite.
- The existing architecture at the Connecticut National Guard already supports VMWare
- It may not be useful to deploy labtainers on the CTNG's architecture if it can be easily deployed on each user's machine locally.
