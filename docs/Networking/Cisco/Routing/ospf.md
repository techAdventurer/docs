# OSPF

#### Enable OSPF on the router:
```cisco
(config)# router ospf {ospf_process_id}
```
#### Specify OSPF interfaces by using one of the following two commands:

On each OSPF-enabled interface, type:
```cisco
(config-if)# ip ospf {ospf_process_id} area {ospf_area_id}
```
Use the network command:

```cisco
(config-if)# network {ip_address}
```
#### Define passive interface to avoid broadcasting OSPF updates to external networks:
```cisco
(config)# router ospf {ospf_process_id}
(config-router)# passive-interface {interface_to_disable}
