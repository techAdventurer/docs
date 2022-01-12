# Cisco basics

## Connect to a device
This section assumes you own some sort of USB to CONSOLE adapter.

### From Windows
1. Connect the cable
2. Open the Device Manager. Under "Ports (COM and LPT), the adapter should be visible as COMx. If it's not, the adapter may need additionnal drivers.
3. Open Putty, select the "Serial" connection type and input the correct COM name (i.e. COM5) in "Serial line".
4. Click on "Open". A new window should open. Press the `ENTER` key to see a prompt.

### From Linux
1. Connect the cable
2. Install the `screen` package
   ```bash
   sudo apt update
   sudo apt install screen
   ```
3. Determine the port of the serial cable using dmesg. It should give a port name similar to `ttyUSB0`
   ```bash
   sudo dmesg | grep -i tty
   ```
4. Connect to the terminal using the following command
   ```bash
   screen /dev/ttyUSB0
   ```
5. Press the `ENTER` key to see a prompt.

## Reset a cisco device
Note the commands below do not erase *everything*.
### Reset a switch
1. Turn on the switch while pressing on the `Mode` physical button on the switch.
2. Release the button when a line is visible on the console.
3. Select `flash_init` (write it then press `ENTER`)
4. Remove all configuration files
   ```
   del flash:vlan.dat
   del flash:config.text
   ```
5. Reboot
   ```
   boot
   ```

### Reset a router
1. Start the router and, within 60 seconds, press `CTRL`+`BREAK` to access the rommon.
2. Modify the config register to ignore the startup-config file at startup.
   ```
   confreg 0x2142
   ```
3. Reboot
   ```
   reset
   ```
4. Check with show running-config that the router has started without configuration.
5. Restore the original value of the config register
   ```
   config-register 0x2102
   ```
6. Save the blank config into the startup-config so the devices restarts into a blank state (restarting before saving will just make the device startup with the old configuration).
   ```
   copy startup-config running-config
   ```
### Reset a device in Packet Tracer

1. Use one of the following commands in enable mode
   ```
   erase startup-config
   ```
   ```
   write erase
   ```
2. Reboot
   ```
   reload
   ```

## Basic commands
Access privileged mode
```
> enable
```

Enable/disable debug
```
# [no] debug [?]
```

Show running-config
```
# show running-config
```

List files in current directory
```
dir
```

## Basic configuration

Disable DNS research (easier for testing in a lab)
```
(config)# no ip domain-lookup
```

Change hostname
```
(config)# hostname {new_hostname}
```

Change MOTD
```
(config)# banner motd {end_char}
```

Set console password:
```
(config)# line console 0
(config-line)# password {password}
(config-line)# login
```

Set `enable` password:
```
(config)# enable secret {password}
```

Encrypt passwords
```
(config)# service password-encryption
```


Save the new configuration
```
# copy running-config startup-config
```

## Configure remote access

1. Configure identification info (used during key generation)
```
(config)# hostname {new_hostname}
```
2. Enable ssh version 2
```
(config)# ip ssh version 2
```
3. Generate key
```
# crypto key generate rsa
```
4. Create an account (example with all privileges)
```
(config)# username {username} privilege 15 secret {password}
(config)# line vty 0 15
(config-line)# transport input ssh
(config-line)# login local
```
5. Test from a Packet Tracer computer
```
ssh -l {device_account} {device_IP}
```

