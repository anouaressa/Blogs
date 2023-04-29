# Introduction to Netfilter and Iptables

### Netfilter :
is a framework in the Linux kernel that provides packet filtering and network address translation (NAT) functions for IPv4 and IPv6 protocols. It's responsible for filtering and manipulating network traffic based on a set of predefined rules.


### Iptables :
is a command-line utility that uses the Netfilter framework to configure the packet filtering rules in the Linux kernel's firewall. It allows administrators to control incoming and outgoing traffic to and from a server or network by defining rules that accept, drop, or redirect packets based on various criteria such as protocol type, source IP address, destination port, and more.


## basic concepts related to Netfilter and Iptables:

### 1 Chains: 
A chain is a sequence of rules that defines how packets should be handled. There are three built-in chains in iptables: INPUT, OUTPUT, and FORWARD. Each chain corresponds to a different stage of packet processing: incoming packets to the local host (INPUT), outgoing packets from the local host (OUTPUT), and packets routed through the host (FORWARD).

### 2 Rules:
 A rule is a set of criteria that a packet must meet in order to be accepted, dropped, or redirected. Each rule is composed of a set of match criteria and a target action. Match criteria can include information such as the source or destination IP address, the protocol used, or the source or destination port number. Target actions can include accepting the packet, dropping it, or redirecting it to another port or IP address.

 ### 3 Tables:
  Tables are collections of chains. There are four tables in iptables: filter, nat, mangle, and raw. The filter table is used for packet filtering, the nat table is used for network address translation, the mangle table is used for more advanced packet manipulation, and the raw table is used for configuring exemptions to connection tracking.

### 4 Policies: 
A policy is a default rule that is applied when no other rules match. Policies can be used to allow or block all traffic by default, or to redirect traffic to a different port or IP address.

### 5 Connection tracking: 
Connection tracking is a mechanism that allows iptables to keep track of the state of network connections. This enables the firewall to allow traffic that is part of an established connection, while blocking traffic that is not. Connection tracking is enabled by default in iptables.

### 6 Targets:
 Targets are the actions that are taken when a rule matches. Targets can include ACCEPT (allow the packet), DROP (drop the packet), REJECT (drop the packet and send a message back to the sender), LOG (log the packet), or MASQUERADE (rewrite the source IP address of a packet to match the outgoing interface).


 # Basic commands for using iptables

 #### 1 View the current iptables rules:*

 
  `sudo iptables -L `
  `sudo iptables -L -n -v`

 *The first command displays the current iptables rules in a readable format. The second command displays the rules in a more detailed format, including numeric IP addresses and packet/byte counters.*

 #### 2 Flush/delete all iptables rules:
  `sudo iptables -F `

  *This command flushes (deletes) all current iptables rules.*

  #### 3 Set a default policy for a chain:
  ` sudo iptables -P INPUT DROP `

  *This command sets the default policy for the INPUT chain to DROP, which means all incoming traffic will be dropped unless a rule explicitly allows it.*

  #### 4 Allow incoming traffic on a specific port:

  `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`

  *allows incoming traffic on TCP port 22 (SSH) in the INPUT chain.*

  #### 5 Block incoming traffic from a specific IP address:

  `sudo iptables -A INPUT -s 192.168.0.100 -j DROP`

  *This command blocks all incoming traffic from the IP address 192.168.0.100 in the INPUT chain.*

  #### 6 Allow outgoing traffic to a specific IP address:

  `sudo iptables -A OUTPUT -d 8.8.8.8 -j ACCEPT`

* allows outgoing traffic to the IP address 8.8.8.8 in the OUTPUT chain.*

#### 7 Redirect incoming traffic to a different port:

`sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080`

*This command redirects all incoming traffic on TCP port 80 to port 8080 using the NAT table*


# Conclusion:

Netfilter and iptables are powerful tools for managing network traffic on Linux systems. By defining a set of rules, you can secure your network, control bandwidth, and prioritize traffic. 


