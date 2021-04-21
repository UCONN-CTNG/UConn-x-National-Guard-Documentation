---
layout: default
title: "VM Deployment Process"
permalink: /vm_deployment_process/
date: 2020-11-22
author: Tim Bogues
---
# VM Deployment Process
#### By: Tim Bogues
VMware vCenter includes APIs that allow for the automated deployment of VMs and applications. The APIs are packaged as a module called [PowerCLI](https://code.vmware.com/docs/12648/powercli-12-1-0-user-s-guide) that runs on top of Microsoft PowerShell, which is available on Windows, Linux, and macOS operating systems. Before diving into an overview of the deployment process, there are a couple of important concepts that need to be introduced. They are VM templates and VM customization specifications.

A VM template is a master image that contains an operating system pre-installed and potentially other components. Templates are typically made by building out a small, base VM that contains a desired operating system (such as Windows Server or Linux). If there are other components that need to always be available on every VM you would like to create based off of this template, then those components/applications could be installed on this base VM as well. After installing/configuring the VM how it should be, then the VM gets powered off. From there, there is an option in vCenter called Convert to Template, which allows that VM to be converted into a template file. This main difference between a template and a normal VM is that a template cannot be powered on and utilized as is. It must either be cloned into a new VM or converted from a template back into a VM.

A VM customization specification is a series of settings/steps that can be applied to new VMs being deployed from a VM template. When someone goes to clone a new VM from a template, they receive the option to select a customization specification to be followed once the VM is powered on for the first time. Common steps included here are setting the hostname, IP address, activating the Windows license if it is a Windows VM, and joining/binding to an Active Directory domain. These customization specifications are very useful, so that such “standard operating procedures” do not need to be re-implemented as custom API calls. VMware vCenter has built in APIs that are able to handle such standard tasks automatically.

At the start of every VM deployment, a connection has to be made to vCenter using the credentials provided. The PowerCLI command for that is:
```
Connect-VIServer -Server $vCenterHostName
```
“$vCenterHostName” refers to the hostname of the vCenter being connected to. From there, the following basic parameters will need to be provided (either as variables or strings in-line): VM name, template name, VLAN, ESXI host to provision VM on, datastore (disk location where VM will be created), folder (folder in vCenter where the VM should be placed...this is purely for organizational purposes), customization specification (if used), IP address (if setting a static IP address...not needed for DHCP - dynamic host configuration protocol), subnet mask (also needed if setting a static IP), gateway address (also needed if setting a static IP), and DNS server(s) (also needed if setting a static IP). All of these parameters can be gathered either from within vCenter or via the network diagrams above. An operating system can also be specified, or that can just be derived from the template. For demo 1, the latter was done.

More information on the VMware infrastructure and available resources can be found here: [https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation/infrastructure_overview/](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation/infrastructure_overview/).

More information on the network infrastructure and available VLANs/IP subnets can be found here: [https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation/network_overview/](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation/network_overview/).

After all of the variables are set, then if using a static IP address and a customization specification, then the next step is to create a temporary specification containing the static IP address information specified in the variables previously. The commands for that go as follows:
```
$custSpec = New-OSCustomizationSpec -Name tempDeploy -Type NonPersistent -OSCustomizationSpec $custSrc
```
```
Get-OSCustomizationSpec $custSpec | Get-OSCustomizationNicMapping | Set-OSCustomizationNicMapping -IpMode UseStaticIP -IpAddress $ipAddress -SubnetMask $subnetMask -DefaultGateway $gateway -Dns $DNS
```
“$custSpec” is the variable containing the temporary specification, “tempDeploy” is the name of the temporary specification, and “$custSrc” is the variable containing the specification used to create the temporary one from.

After the temporary customization specification is created, then the next step is to actually deploy/clone a new VM from a template. The command for that is as follows:
```
New-VM -Name $vmName -Template $vmTemplate -NetworkName $vmVLAN -OSCustomizationSpec $custSpec -VMHost $vmHost -Datastore $vmDatastore -Location $vmFolder
```
Once the VM finishes provisioning, then it can be powered on with the following command:
```
Start-VM $vmName
```
From there, the VM will power on and complete any actions specified in the customization specification. One mechanism that can be used to determine when the customization is complete is to check when the VM’s hostname equals the VM name. Once it does, then the VM has been named appropriately, and the customization is complete. From there, any commands that need to be run on the VM’s operating system in order to install/configure additional components can be run inside of an “Invoke-VMScript” command. This works by communicating with the VMware guest tools that are pre-installed on the VM as part of creating the template as well as specifying credentials to access the VM with. An example of this command is as follows:
```
Invoke-VMScript -VM $vmName -ScriptText ‘Insert Command Line Text Here’ -ScriptType Powershell
```
“-ScriptText” is where the command to be run on the VM’s OS is specified and “-ScriptType” is where the type of command line interface should be specified. Options for this include PowerShell, Bat (Windows Command Prompt), and Bash (Linux). After all of the desired commands have been run on the VM’s OS, then the VM is finished deploying and should be available to be used.


[Main Menu](https://uconn-ctng.github.io/UConn-x-National-Guard-Documentation)
