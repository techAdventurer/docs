# Network configuration

## Configuring interfaces

Set a description to the interface:
```
(config-if)# description {interface_description}
```

### IPv4

Add an IPv4 address to an interface:
```
(config-if)# ip address {ipv4_address} {netmask}
```

Add a default gateway:
```
(config-if)# ip default-gateway {ipv4_address}
```

Enable the interface:
```
(config-if)# no shutdown
```

### IPv6

Enable IPv6:
```
(config)# ipv6 enable
```

Enable IPv6 routing:
```
(config)# ipv6 unicast-routing
```

Add an IPv6 address to an interface:
```
(config-if)# ipv6 address {ipv6_address}/{short_netmask} {eui-64/link-local}
```

Enable the interface:
```
(config-if)# no shutdown
```


## Configure static routes

Show routes:
```
# show ip route
```

### IPv4
Configure a route via a next hop ("recursive") or interface:
```
(config)# ip route {network_to_reach} {netmask} {nexthop_ip/interface_name}
```

Configure a default route:
```
(config)# ip route 0.0.0.0 0.0.0.0 {nexthop_ip/interface_name}
```

### IPv6
Configure a route via a next hop or interface:
```
(config)# ipv6 route {network_to_reach}/{short_netmask} {nexthop_ip/interface_name}
```

Configure a default route:
```
(config)# ipv6 route ::0/0 {nexthop_ip/interface_name}
```

## Floating routes

Do not forget to save the configuration!
