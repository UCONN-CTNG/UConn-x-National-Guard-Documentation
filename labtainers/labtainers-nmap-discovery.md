---
layout: default
title: "Labtainers nmap-discovery Walkthrough"
permalink: /labtainers/nmap-discovery/
date: 2020-11-22
author: Chris
---

# Labtainers nmap-discovery Walkthrough

---

### Step-by-step Guided walkthrough

First, launch the nmap-discovery lab, and open the corresponding pdf, using the

```
labtainers nmap-discovery
```

command, as denoted in the [quickstart guide](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation/labtainers/quickstart/).

After hitting enter to start the lab, two new terminal windows should appear, one of which containing instructions for the lab, and the other of which containing the phrase

```
ubuntu@my-computer:~$
```

and an empty prompt.

Take a moment to read through the pdf and xterm instructions.
According to these documents, the goal of this exercise is to find an ssh server located somewhere on the network, and then to login to it.

It's clear that we want to use nmap to scan the network for nearby servers.
There are multiple steps to this process.

First, we need to determine the ip address range we want to scan:

We can determine our current ip address using the `ip addr` command.


We want to scan as many nearby ip addresses as possible. IP addresses on the same subnet share the same almost the exact same address, except for the last number of the IP.

The range of IP's in the same subnet look like this: `172.25.0.1-255`

Once we have the range of ip addresses we want to scan, we can use nmap to scan them.

```
nmap -sn 172.25.0.1-255
```
Now, we know the IP of another host on the network.

We can scan a range of ports on this host using nmap.
If the server has a port open, we can try to ssh through that port.

```
ssh 172.25.0.5 -p 2858
```

We can then use the password given in the problem description to login.

Once you're finished with the lab, you can use the `stoplab` command to dismantle the network and save your progress.

---

### Video Walkthrough (begins at about halfway).

<iframe width="560" height="315" src="https://www.youtube.com/embed/qP2htZD7gao" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

