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
For this post, you will need three things: <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
1- Router that has public IP.  <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
2- Virtual machine that has docker installed and has access to the internet.  <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
3- Registered domain name through Cloudflare. <br />

#  **Terminology**

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Before diving into the project, let's take a define some terms to establish ground-level of knowledge:
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/CF_dashboard.png"/>
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
`Cloudflare Dashboard`: Cloudflare dashboard is where you define the DNS records and modify them. Since we're on the subject, the dashboard so many many AMAZING services that I can't even begin to fathom what you could accomplish with them. For the time being, we will stick with the basics ones such as:
<br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> 1- DNS: To define our DNS records <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> 2- SSL/TLS: To modify TLS negotiations with the proxy and other parties. <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.1em;"> 3- Access: Protect internal resources by requiring authentication <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.1em;"> To read more about these services, visit their [documentation]( https://support.cloudflare.com/hc/en-us/articles/205075117-Understanding-the-Cloudflare-dashboard) page.
<span style="color: #f2cf4a; font-family: Babas; font-size: 1.1em;">  
`Traefik`: Traefik is a dockerized and open-source reverse proxy and load balancer typically used for microservices.
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/Traefik.png"/>
</span>

##  **Install/Setup**
### - Cloudflare Setup


### - VM setup
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
After we install the dependencies namely docker and docker-compose in the VM.
Open the terminal in you VM and clone this repo:  <br />
`root$ git clone https://github.com/sh1dow3r/Traefik_CF`  <br />
`root$ cd Trafik_CF`
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Inside the repo you will need to apply two task
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
1- Generate a certificate for Traefik microserviec and place it in certs directory, which can be easily done with this command  <br />
`mkdir -p certs; openssl req -x509 -newkey rsa:4096 -nodes -out certs/cert.crt -keyout certs/cert.key -days 365`  <br />
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
2- Make note of your Global API KEY and email from your cloudflare account. This information can be found in your under your profile [Cloudflare dashboard]( https://dash.cloudflare.com/)  <br />
After you have taking the global API Key, add it to the dockerfile in Traefik folder, and add your email as well as shown in the screenshot below:
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/CF_API.png"/>
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/Traefik_Dockerfile.png"/> 


### - Pfsense Setup

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">  
Now that we configure Pfsenes to redirect the traffic coming on port 80 and port 443 of the public IP to be redirected to the Traefik reverse proxy. That will be quickly done through the NAT rule to allow port forwarding and through the Firewall Rules to allow incoming traffic to come in.  
</span>
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
The Firewall rules would look like something like this:
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/FirewallRule.png"/> 
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
The NAT rules would look like something like this:
<img src="https://raw.githubusercontent.com/sh1dow3r/layer0/gh-pages/_posts/img/Remote_Access_Homelab/NATRule.png"/> 



## Conclusion

<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;">
 Cloudflare and Traefik </span >

# References


[Cloudflare docs](https://support.cloudflare.com/hc/en-us/articles/205075117-Understanding-the-Cloudflare-dashboard)

[Cloudflare Settings for Traefik Docker](smarthomebeginner.com/cloudflare-settings-for-traefik-docker/)

[Evan's Github](https://github.com/egallis31/traefik-elk-grafana)
