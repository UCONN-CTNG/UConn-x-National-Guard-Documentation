---
layout: default
title: "Labtainers Developer Walkthrough"
permalink: /labtainers/developer/
date: 2020-11-22
author: Chris
---

# Labtainers Developer Walkthrough

The labtainers development environment can be set up rather simply by running the ~/labtainer/update-designer.sh script (when sudo access is required, use `password123`).

More information about developing a new lab can be found [here](https://nps.box.com/shared/static/12n0y4yue49xcxtpv0jybgqiiskx8pr6.pdf)

A new lab can be created by following these steps:

1. Create a new director for the lab in the `/home/labtainer/student/trunk/labs` folder, and enter it. You might want to observe other lab folders to get a sense for how other labs were created.

2. Run the `new_lab_setup.py` script, which will generate template files which can be edited to configure the lab.

3. Open a new terminal and navigate to the `labtainer-student` directory. From here you can launch the lab using the `rebuild LABNAME` command. It's necessary to navigate to the `labtainer-student` directory, since labs can only be started from this folder.

4. Stop the lab with `stoplab` and navigate to the `/home/labtainer/student/trunk/labs/LABNAME/LABNAME` directory.

5. In this directory you can add new files, which will also be added to the container when it launches. You can also add files to the `_system` directory, which will then be added to the container on boot. For example, if the file `hello` is added to `_system/usr/bin/`, then the file `/usr/bin/hello` will be added to the container on boot.

6. Additionally, commands can be added to the `_bin/fixlocal` script to run commands in the container immediately after the container spins up, but before the user is allowed to access it.

7. Finally, another container can be added to the lab by using the `new_lab_setup.py -a new_container` command. When the lab starts, the user will be able to view and run commands in a terminal corresponding to this new container.
