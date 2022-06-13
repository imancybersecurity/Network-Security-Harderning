![Simple_Network_Harderning](https://user-images.githubusercontent.com/106005322/173357304-0c2f27e6-20ff-48a7-b867-01c8f0a47f13.png)

<img alt="YouTube Video Views" src="https://img.shields.io/youtube/views/IXY1sUxyufM?style=social">

![abb53b70f9b97c01a4f700f4a8348444](https://user-images.githubusercontent.com/106005322/173247515-74f66a04-aae3-4c68-9e7e-400c1fbd867a.gif)

Assalamualaikum Warahmatullahi Wabarakatuh, so now i will explain a simple or easy Harderning related to Networking (sysctl.conf)

### sysctl is an interface that allows you to make changes to a running Linux kernel. With /etc/sysctl.conf you can configure various Linux networking and system settings such as:

* Reverse Path Filtering
* TCP/IP SYN cookies
* IP Forwarding for IPv4 & IPv6
* Accept Redirects
* Secure Redirects
* Send Redirects
* Accept Source Route


### Sample /etc/sysctl.conf for Ubuntu 22.04 LTS
```python
#/etc/sysctl.conf - Configuration file for setting system variables. 
#See /etc/sysctl.d/ for additional system variables. 
#See sysctl.conf (5) for information. 

#kernel.domainname = example.com

#Uncomment the following to stop low-level messages on console 
#kernel.printk = 3 4 1 3

###################################################################
#Functions previously found in netbase

#Uncomment the next two lines to enable Spoof protection (reverse-path filter)
#Turn on Source Address Verification in all interfaces to
#prevent some spoofing attacks
#net.ipv4.conf.default.rp_filter=1
#net.ipv4.conf.all.rp_filter=1

#Uncomment the next line to enable TCP/IP SYN cookies
#See http://lwn.net/Articles/277146/
#Note: This may impact IPv6 TCP sessions too
#net.ipv4.tcp_syncookies=1

#Uncomment the next line to enable packet forwarding for IPv4
#net.ipv4.ip_forward=0

#Uncomment the next line to enable packet forwarding for IPv6
#Enabling this option disables Stateless Address Autoconfiguration
#based on Router Advertisements for this host
#net.ipv6.conf.all.forwarding=1


###################################################################
#Additional settings - these settings can improve the network 
#security of the host and prevent against some network attacks
#including spoofing attacks and man in the middle attacks through
#redirection. Some network environments, however, require that these
#settings are disabled so review and enable them as needed.
#
#Do not accept ICMP redirects (prevent MITM attacks)
#net.ipv4.conf.all.accept_redirects = 0
#net.ipv6.conf.all.accept_redirects = 0
#_or_<br>
#Accept ICMP redirects only for gateways listed in our default
#gateway list (enabled by default)
#net.ipv4.conf.all.secure_redirects = 1
#
#Do not send ICMP redirects (we are not a router)
#net.ipv4.conf.all.send_redirects = 0
#
#Do not accept IP source route packets (we are not a router)
#net.ipv4.conf.all.accept_source_route = 0
#net.ipv6.conf.all.accept_source_route = 0
#
#Log Martian Packets
#net.ipv4.conf.all.log_martians = 1
#

###################################################################
#Magic system request Key
#0=disable, 1=enable all, >1 bitmask of sysrq functions
#See https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html
#for what other values do
#kernel.sysrq=438
```
### STEP BY STEP CONFIGURATION

#### Example usage
```python
# check all existing sysctl parameters
$ sysctl -a
 
# change them temporary
$ sudo net.ipv4.conf.default.rp_filter=1
 
# change them permanently 
$ vim /etc/sysctl.conf
# edit
...
# load 
$ sysctl -p /etc/sysctl.conf
```
#### Reverse Path Filtering
Reverse path filtering is a mechanism adopted by the Linux kernel, as well as most of the networking devices out there to check whether a receiving packet source address is routable. So in other words, when a machine with reverse path filtering enabled receives a packet, the machine will first check whether the source of the received packet is reachable through the interface it came in. If it is routable through the interface which it came, then the machine will accept the packet.
If it is not routable through the interface, which it came, then the machine will drop that packet.
```python
#IPv4
$ sysctl -w net.ipv4.conf.default.rp_filter=1
#IPv6
$ sysctl -w net.ipv4.conf.all.rp_filter=1
```

#### TCP/IP SYN cookies 
SYN cookies is an IP Spoofing attack mitigation technique whereby server replies to TCP SYN requests with crafted SYN-ACKs, without creating a new TCB for the TCP connection. A TCB is created for the respective TCP connection only when the client replies to this crafted response. This technique is used to protect the server’s resources from filling up under TCP SYN floods.
```python
$ sysctl -w net.ipv4.tcp_syncookies=1 
```

#### IP Forwarding for IPv4 & IPv6
You can configure your Linux distribution to function as a router and connect different networks together. To do this, you need to enable IP forwarding in the configuration file.
```python
#IPv4
$ sysctl -w net.ipv4.ip_forward=0

#IPv6
$ sysctl -w net.ipv6.conf.all.forwarding=0
```

#### Accept Redirects
Redirects let one machine tell another machine to route traffic through a node other than what's in its routing table.
```python
#IPv4
$ sysctl -w net.ipv4.conf.all.accept_redirects=0

#IPv6
$ sysctl -w net.ipv6.conf.all.accept_redirects=0
```

#### Secure Redirects
Prevents hijacking of routing path by only allowing redirects from gateways known in our routing table.
```python
$ sysctl -w net.ipv4.conf.all.secure_redirects=1
```

#### Send Redirects
This command disables sending of all IPv4 ICMP redirected packets on all interfaces
```python
$ sysctl -w net.ipv4.conf.all.send_redirects=0
```

#### Accept Source Route
Source routing is an Internet Protocol mechanism that allows an IP packet to carry information, a list of addresses, that tells a router the path the packet must take. There is also an option to record the hops as the route is traversed. The list of hops taken, the "route record", provides the destination with a return path to the source. This allows the source (the sending host) to specify the route, loosely or strictly, ignoring the routing tables of some or all of the routers. It can allow a user to redirect network traffic for malicious purposes. Therefore, source-based routing should be disabled.
```python
#IPv4
$ sysctl -w net.ipv4.conf.all.accept_source_route=0

#IPv6
$ sysctl -w net.ipv6.conf.all.accept_source_route=0
```




