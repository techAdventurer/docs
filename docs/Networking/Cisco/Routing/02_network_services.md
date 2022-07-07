# Network services

## DHCP
Create a DHCP pool
```
(config)# ip dhcp pool {dhcp_pool_name}
```

Set a network for the dhcp pool
```
(dhcp-config)# network {network_ip} {netmask}
```

Exclude some addresses from the pool (so they are not assigned)
```
(config)# ip dhcp excluded-address {address_to_exclude (? for more options)}
```

Set default gateway
```
(dhcp-config)# default-router {gateway_ip_address}
```

Set the DNS server
```
(dhcp-config)# dns-server {dns_ip_address}
```

Useful debugging commands:
```
# show running-config
# show ip dhcp binding
# show ip dhcp pool
# show ip dhcp conflict
```
