---
layout: default
title: "Scenario1 Login Solutions"
permalink: /scenario1/login_solutions/
date: 2020-11-22
author: Vinh
---
# Login Solutions:

# Approach 1 - MySQL:

One possible approach we looked at was using a MySQL database to store all the usernames and passwords. This would have allowed us to create a vulnerability in the login procedure to SQL Injections that would allow us to simulate an attack. MySQL was an accessible option for us to use, very simple to set up and most of us had experience with it. The issue we ran into with using MySQL was that there was no easy way to link it up with Active Directory. For future extensions of this scenario or in another scenario, it may be worthwhile to look further into using MySQL and possibly using third-party extensions that would allow for linking MySQL with Active Directory. This would be beneficial if there are certain real world cases in which the MySQL database is used that the National Guard would prefer to train with. 

When creating our demo using MySQL, we manually create a MySQL database with different usernames and passwords. Our database table only had two columns, usernames and passwords. The Apache Web Server was set up with a login page that would take in input for a user’s username and password. The user would then be redirected to a welcome page. In order to allow unintended users to access the database, we included requests to the MySQL database with unsanitized inputs. This would allow SQL injection attacks to be performed. This means a malicious actor would be able to include SQL code into their inputs in order to improperly access the database. For example, one attack we focused on was one where the attack would be able to type in ' or '1'='1 into the username or password field in order to access the system without the proper credentials. This is able to occur since we are querying the database with a query that looks like this, `'SELECT * FROM Users WHERE Username = ' + Username;` The attack would turn the query into `'SELECT * FROM Users WHERE Username = '' or '1'='1;` , which will always allow access since `‘1’ = ‘1’` is always true. Using this exploit allows people to get to the welcome page, even without a valid username and password. 

# Approach 2 - LDAP (Lightweight Directory Access Protocol): 

LDAP is a protocol that allows users to access directory services such as Windows Active Directory. This allows us to use the authentication and user control methods built into Active Directory to control logins. Not only does this allow for us to have different users and passwords for each user, it also allows us to enable logging within our Active Directory system so that members of the National Guard can see where there might be suspicious behavior. Setting up user accounts on Active Directory was intuitive and fairly simple. However, the team did not have much experience with using LDAP and there was a learning curve when working with it. 

When creating the demo using LDAP and Active Directory, we created users within the Active Directory system that we would be able to login with. The login process was identical to the one used for MySQL, except it made queries to the Active Directory we set up instead of a MySQL database. The usernames and passwords were the ones set up for users in the Active Directory system, and it also allowed us to keep logs of login and logouts from various users. It was also set up such that users had different levels of access within the system. A regular user would be sent to a regular welcome page after logging in, but an administrator would be sent to a page with information queried from the Active Directory. Although we did attempt to create a similar injection vulnerability for the login system, we found an easier way to keep the system unsecure was to allow for anonymous binding. This made it so that not including a password would allow a user to login anonymously. However, this also did not prevent anybody simply accessing the administrator webpage by using the admin username without a password. By using anonymous binding, anybody is able to access information not intended for them as long as they had the correct username. With the help of the logs  within Active Directory, it is possible to see if there is suspicious activity. 

[Main Menu](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation)

Author: Vinh
