# SIMPLE GARDERNING NETWORK

![abb53b70f9b97c01a4f700f4a8348444](https://user-images.githubusercontent.com/106005322/173247515-74f66a04-aae3-4c68-9e7e-400c1fbd867a.gif)

Assalamualaikum Warahmatullahi Wabarakatuh, so now i will explain a simple or easy Harderning related to Networking (sysctl.conf)

### sysctl is an interface that allows you to make changes to a running Linux kernel. With /etc/sysctl.conf you can configure various Linux networking and system settings such as:

* Limit network-transmitted configuration for IPv4
* Limit network-transmitted configuration for IPv6 
* Turn on execshield protection 
* Prevent against the common ‘syn flood attack’
* Turn on source IP address verification 
* Prevents a cracker from using a spoofing attack against the IP address of the server 
* Logs several types of suspicious packets, such as spoofed packets, source-routed packets, and redirects.

# Sample /etc/sysctl.conf for Ubuntu 22.04 LTS

#/etc/sysctl.conf - Configuration file for setting system variables. <br>
#See /etc/sysctl.d/ for additional system variables. <br>
#See sysctl.conf (5) for information. 

#kernel.domainname = example.com

#Uncomment the following to stop low-level messages on console <br>
#kernel.printk = 3 4 1 3

###################################################################<br>
#Functions previously found in netbase

#Uncomment the next two lines to enable Spoof protection (reverse-path filter)<br>
#Turn on Source Address Verification in all interfaces to<br>
#prevent some spoofing attacks<br>
#net.ipv4.conf.default.rp_filter=1<br>
#net.ipv4.conf.all.rp_filter=1

#Uncomment the next line to enable TCP/IP SYN cookies<br>
#See http://lwn.net/Articles/277146/<br>
#Note: This may impact IPv6 TCP sessions too<br>
#net.ipv4.tcp_syncookies=1

#Uncomment the next line to enable packet forwarding for IPv4<br>
#net.ipv4.ip_forward=0

#Uncomment the next line to enable packet forwarding for IPv6<br>
#Enabling this option disables Stateless Address Autoconfiguration<br>
#based on Router Advertisements for this host<br>
#net.ipv6.conf.all.forwarding=1


###################################################################<br>
#Additional settings - these settings can improve the network<br>
#security of the host and prevent against some network attacks<br>
#including spoofing attacks and man in the middle attacks through<br>
#redirection. Some network environments, however, require that these<br>
#settings are disabled so review and enable them as needed.
#
#Do not accept ICMP redirects (prevent MITM attacks)<br>
#net.ipv4.conf.all.accept_redirects = 0<br>
#net.ipv6.conf.all.accept_redirects = 0<br>
#_or_<br>
#Accept ICMP redirects only for gateways listed in our default<br>
#gateway list (enabled by default)<br>
#net.ipv4.conf.all.secure_redirects = 1<br>
#
#Do not send ICMP redirects (we are not a router)<br>
#net.ipv4.conf.all.send_redirects = 0
#
#Do not accept IP source route packets (we are not a router)<br>
#net.ipv4.conf.all.accept_source_route = 0<br>
#net.ipv6.conf.all.accept_source_route = 0
#
#Log Martian Packets<br>
#net.ipv4.conf.all.log_martians = 1
#

###################################################################<br>
#Magic system request Key<br>
#0=disable, 1=enable all, >1 bitmask of sysrq functions<br>
#See https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html<br>
#for what other values do<br>
#kernel.sysrq=438

# STEP BY STEP CONFIGURATION

## Enable/Disable packet forwarding for IPv4

How to check the status of ip forward whether enable or disable there are two commands<br>
 cat/proc/sys/net/ipv4/ip_forward<br>
 sysctl net.ipv4.ip_forward

How to setup temporarily disable or enable<br>
 echo 1>/proc/sys/net/ipv4/ip_forward<br>
 sysctl -w net.ipv4.ip_forward = 1
 
The way to setup disable or enable it by editing it permanently<br>
 nano /etc/sysctl.conf<br>
 Uncomment hashtags to enable edit<br>
 To enable the changes made in sysctl > sysctl -p /etc/sysctl.conf 
 







