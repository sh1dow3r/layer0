---
layout: post
title:  "Virtualized Malware Analysis Environment"
categories: Malware_Forensics
---

<span style="color: #f2cf4a; font-family: Babas; font-size: 1.2em;">
Recently, I have been involved in a lot of projects related to DevOps and building secure infrastructure as Code (IAC) which I will be blogging about once I finish them. In this blog I'll go over basic tools I have used to accomplish this project.  
</span>

## **Background**

### Cuckoo Sandbox Project
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.2em;">

Cuckoo Sandbox project is an open-sourced tool that automates dynamic malware analysis. The project was built using python language which makes the installment process easier to install across all platform. Cuckoo also supports malware analysis on Windows, OSX, Linux, and Android. Cuckoo, also, have a well-defined structure that makes it easy to customize. This feature has allowed analysts across the world to add custom modules and plugins that capture certain artifacts to result the best outcome. Lastly, Cuckoo have a great community support for the project which beyond the scope of this blog but could be found on this github repo. https://github.com/cuckoosandbox/community
</span>

### SIFT Workstation
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.2em;">

SIFT Workstation is a powerful forensics framework that contains most of the open-source tools used by industry-level analysts. SIFT workstation comes in the form of an appliance and could be ran as a virtual machine. Reducing the overhead of installing and configuring each tool is one of its greatest advantage.
</span>

### Ansible
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.2em;">

Ansible is an open-source software and powerful tools that could be used for various aspects. Ansible mainly know for four overall functionality

* Application Deployment (Like Fabic)
* Provisioning (Like Cobbler or JuJu)
* Configuration Management (Like Chef or Puppet)
* Multi-tier Orchestrion (Like Chef-Metal)
 </span>

## Vagrant
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.2em;">

Vagrant is a provisioning platform from hashicorp that is used to spins up and maintain virtual machines in different hypervisor providers such as AWS, VMware and virtualbox.
open keyboard shortcuts file.
</span>

## **Introduction**

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">

Configuring and setting up different services manually is both time-consuming and labor-intensive. In this project,  I tried to implement an automated solution for a malware analyst to deploy a sandboxed environment using different technology. Starting by Ansible scripts that deploy SANS workstation to a VMware vCenter host then deployment Cuckoo sandbox software along with all its required dependencies using ansible. After that, I used Vagrant to build a virtual machine (In my case, I 'll be using Windows 10, however, there is plenty of supported OS), to be used for my malware analysis.    </span>

#    **Constructed Topology**

<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/Virtualized_Malware_Analysis_Environment.png"/>

#  **Install/Setup**

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Before diving into the project let's take a quick look at the structure of the code:   
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/Sandboxer_Dir_Structure.png"/>    

As you can here, we have a bunch of files, starting from the top, we have:  
`Sandbox-Playbook.yml`: which contains the overall tasks(roles) to be executed against our machine.  
`inventory.ini`: contains the variables used to communicate with the other  node such IP, user and password of the client machine  
`roles`: the different subtask of the project  
`roles\SIFT-Cuckoo-Sandbox`: subtask to install and configure Cuckoo sandbox project  
`roles\SIFT-Deploy`: subtask to deploy SIFT workstation to vCenter
`vars.yml`: a centralized place to hold all the variables of the project.


`git clone https://github.com/sh1dow3r/SandBoxer` 
`cd SandBoxer`  
Edit `vars.yml` accordingly
</span>

#  **How does it work?**
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
After we setup the project, let 

</span>


# Conclusion
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
Buliding Malware analysis environment mannually requires time and resource and can bee overwhlmening to setup. In this project, I proposed a solution of how easlily to write automated process
</span >

# References


[Port Security Cisco Guied](https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html)

[Vagrant-Virtualbox provider](https://www.vagrantup.com/docs/virtualbox/)

[Cuckoo Ansible example](https://github.com/fyhertz/ansible-role-cuckoo)
