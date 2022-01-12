# Configuring VLANs and interfaces

## VLANs

In the normal range (VLAN ID 1-1005), VLANs config is saved in vlan.dat and VTP (VLAN Trunking Protocol) works. With extended range (VLAN ID 1006-4094), VLANs config is saved in running-config and VTP doesn't work.

Create a vlan:
```
(config)# vlan {vlan_id}
(config-vlan)# name {vlan_name}
```

Assign interfaces to VLANs (VLAN will be created if non-existent):
```
(config)# interface {interface_name}
(config-if)# switchport mode access
(config-if)# switchport access vlan {vlan_id}
```

To select multiple interfaces in a range, use the following syntax:
```
(config)# interface range {interface_name}0/0-20
```

Set an interace as a trunk:
```
(config-if)# switchport mode trunk
```

By default, all VLANs are authorized on the trunk. To white-list VLANs, use the following command:
```
(config-if)# switchport trunk allowed {vlan_id_1},{vlan_id_2}-{vlan_id_10}
```

## Virtual interfaces (management)
To manage the switch from the network, we need to create a Switch Virtual Interface (SVI). There can only be one interface per VLAN. Since the switch will most likely be managed from another network, we also need to configure a default gateway (since the device will most likely not be contained in the switch's ARP table, it must have a default gateway).

Create a SVI:
```
(config)# interface vlan {vlan_id}
(config-if)# ip address {vlan_interface_ip} {netmask}
(config-if)# no shutdown
```

Set default gateway:
```
(config)# ip default-gateway {default_gateway_ip}
```

## Switch security

### Disable useless ports

Shutdown a port:
```
(config-if)# shutdown
```

### MAC-based security

#### Types
MAC-based security on a switch comes down to authrizing a number of MAC addresses on a port. The way the switch learns about those addresses can be one of the following:
- **Static secure MAC addresses**: MAC addresses are entered manually
  ```
  (config-if)# switchport port-security mac-address {mac_address}
  ```
- **Dynamic secure MAC addresses**: MAC addresses are "learned" automatically. Resets if the switch is restarted.
  ```
  (config-if)# switchport port-security mac-address dynamic
  ```
- **Sticky secure MAC addresses**: Combination of the two above. MAC addresses can be added manually and "learned", but they are added to the running-config.

  To activate "sticky learning":
  ```
  (config-if)# switchport port-security mac-address sticky
  ```
  To add a "sticky address" manually:
  ```
  (config-if)# switchport port-security mac-address sticky {mac_address}
  ```

#### Security violations
A security violation happens during one of the following events:
- Maximum number of MAC addresses has been reached or a non-authorized MAC address attempts to access the network
- An authorized MAC address, on a secure port, changes port on the same VLAN (understood as a spoofing attempt)

Consequences of these violations can be one of the following:
- **Protect**: Frames are blocked, silently (no notification)
- **Restrict**: Frames are blacked (notification is sent)
- **Shutdown** (default): Port shuts down. Need to input the commands `shutdown` and `no shutdown` to revive the interface.

To chose a behaviour in response to a security violation, use this command:
```
(config-if)# switchport port-security violation {protect/restrict/shutdown}
```

### DHCP snooping
DHCP snooping is a functionality that blocks DHCP offers from untrusted ports (and more - [see the official documentation](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus3000/sw/security/503_u2_2/Cisco_n3k_security_cg_503_u2_2_chapter10.html)).

Enable DHCP snooping globally (has no effect but is necessary for next step)
```
(config)# ip dhcp snooping
```

enable DHCP snooping for specified VLAN(s)
```
(config)# ip dhcp snooping vlan {vlan_id_1},{vlan_id_10}-{vlan_id_100}
```

Once activated, all interfaces are by default "untrusted". To set an interface as "trusted", use the following command:
```
(config-if)# ip dhcp snooping trust
```


