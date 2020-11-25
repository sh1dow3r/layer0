---
layout: post
title:  "Securing HomeLab Access"
categories: Homelab
---


## **Introduction**

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
If you have wonder if there is a way to access your web console of your homelab hypervisor externally and restrict access to it, this blog is what you are seeking. In this blog, I will show a use case where you can use an open-source reverse proxy alongside Cloudflare "awesome" dashboard functionality.</span>

## What you will need?
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
For this post, you will need two things:
    - Router that has public IP.
    - Virtual machine that has docker installed and has access to the internet.
    - Registered domain name through Cloudflare.
</span>

#  **Terminology**

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Before diving into the project, let's take a define some terms to establish ground-level of knowledge:   </span>
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/CF_dashboard.png"/>

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
`Cloudflare Dashboard`: Cloudflare dashboard is where you define the DNS records and modify them. Since we're on the subject, the dashboard so many many AMAZING services that I can't even begin to fathom what you could accomplish with them. For the time being, we will stick with the basics ones such as:

- DNS: To define our DNS records
- SSL/TLS: To modify TLS negotiations with the proxy and other parties.
- Access
</span>

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
`Traefik`: Traefik is a dockerized and open-source reverse proxy and load balancer typically used for microservices.
</span>


##  **Install/Setup**
### - VM setup
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
After we install the dependencies such docker and docker-compose in the VM.

Open the terminal in you VM and clone this repo:
`root$ git clone https://github.com/sh1dow3r/Traefik_CF`
`root$ cd Trafik_CF` 
In this dicrtory you will need to apply two task
1- Generate a certifacate for Traefik microserviec and place it in certs dircotry, which can be easliy done with this command
`mkdir -p certs; openssl req -x509 -newkey rsa:4096 -nodes -out certs/cert.crt -keyout certs/cert.key -days 365`
2- Add you API_KEY and email from your cloudflare account. This information can be found in your Cloudflare dahshboard  [Cloudflare dahshboard]( https://dash.cloudflare.com/)

<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/SIFT_Deploment_vCenter.png"/>

<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/Ansible_output_after_vcenter_deployment.png"/>
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
As you can see, 

### - Pfsense Setup

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Now that we have deployed the virtual machine, let's starts the the Cuckoo deployment. 
</span>
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/cuckoo_after_installing.png"/> 

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
After we confirmed all the configuration is done, we'll navigate to `home/cuckoo/vagrant_files` which has the windows10 virtual machine we're going to use for malware analysis. There should be a bash script called `vagrant_script.sh` that is going to pull a windows 10 image and set it up with Virtualbox then take a stable snapshot.
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/After_vagrant.png"/> 

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
After windows10 is up and running make sure it's snapshotted and there you go, you have your Cuckoo Sandbox up and ruining! :
</span>
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Sandbox/Cuckoo_up_and_running.png"/> 


## Conclusion

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
Building Malware analysis environment manually requires time, resource and can bee overwhelming to setup. In this project, I proposed a solution of an automated process
to setup you're own malware environment using DevOps tools like Ansible and Vagrant. </span >

# References


[Ansible docs](https://docs.ansible.com/ansible/latest/modules/lineinfile_module.html)

[Vagrant-Virtualbox provider](https://www.vagrantup.com/docs/virtualbox/)

[Cuckoo Ansible example](https://github.com/fyhertz/ansible-role-cuckoo)
