---
layout: default
title: "Scenario 1 Overview"
permalink: /scenario1/overview/
date: 2020-11-22
author: Vinh
---
# Scenario 1 (Web Server Vulnerability):

# Goal:

The goal of this first scenario is to mimic a vulnerable web server that allows for a malicious entity access to secure environments. This would allow for training situations where a web server has been compromised or if another user was accessing accounts not meant for them. This first attempt at creating a training scenario also worked as a technical demonstration for the team’s use of the virtual environment set up for the National Guard’s cyber-range, as well as the use of Active Directory. 

# Use Cases:

Members of the National Guard Cyberdefense team can use this scenario as an entry level training exercise to get acquainted with Active Directory and common practices for analyzing and securing vulnerable systems. 

# Technologies Used:

**Apache Web Server**:  Used to simulate a website with varying levels of access as well as an entry point for users/malicious entities. It is housed on a VM running an Ubuntu Linux OS.

**Active Directory**: A Windows based directory service that can be used to authorize and authenticate users, assign and enforce security policies, log access to various system resources, and other services that may be useful to the management of a Windows based network. This was used to provide authentication for users to Apache Server as well as logging information for user logins/logouts. It is housed on a VM running a Microsoft Windows Server 2012 OS.

**LDAP (Lightweight Directory Access Protocol)**: The protocol used to query Active Directory for user login information. This was used to connect to the Active Directory database and retrieve user information in order to connect to the Apache Server.

**VMWare vSphere**: A cloud computing virtualization platform that allows users to set up and manage various computing resources/infrastructures. This was used to create environments for the Apache Web Server and the Active Directory.

[Main Menu](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation)

Author: Vinh
