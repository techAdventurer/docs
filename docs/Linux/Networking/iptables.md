# IPtables
IPtables is a command-line tool used to create packet-filtering rules using the [netfilter kernel module](https://www.netfilter.org/index.html). This makes it a firewalling software.

Rules are contained in tables, depending on what we mean to do with the packets:
- **FILTER** (default): Contains rules to accept or drop packets
- **NAT**: Contains rules related to NAT
- **MANGLE**: Contains rules to modify a packet (TTL, ...)
- **SECURITY**: Related to SELinux
- **RAW**

**FILTER** and **NAT** are the two most used tables.

Netfilter provides a set of hooks, triggered when packets pass through the Linux network stack (NF_IP_PRE_ROUTING, NF_IP_LOCAL_IN, ...etc). Hooks trigger built-in chains (chains are sequential sets of related rules, inspected one by one until the packet corresponds to the selector), contained inside the tables. Default chains available in the **FILTER** table are **INPUT**, **FORWARD** and **OUTPUT**. Note that it is possible for administrators to create custom chains, and reference it from the built-in rules.

Rules are 

## Main commands
List all the rules in any table:
```bash
sudo iptables -L
```

## Default configuration
- Block everything
- Allow loopback interface
- Allow LAN to WEB
- 

## FILTER table
Lister 

## NAT table

## Custom chains
