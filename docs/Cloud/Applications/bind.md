# DNS with bind 9

## Installing bind on Linux
### Debian-based
```bash
sudo apt update
sudo apt install --yes \
    bind9 \
    bind9-utils \
    bind9-doc
```

### Fedora
```bash
sudo dnf install -y \
    bind \
    bind-utils
```

Configuration files are either accessible in `/etc/` or `/etc/bind/`:
- `./named.conf` (server configuration file - see `man named.conf`)
- `./named/` (contains the configuration files for zones)


## Server configuration



 

## See also
- https://www-uxsup.csx.cam.ac.uk/pub/doc/redhat/redhat7.3/rhl-rg-en-7.3/s1-bind-configuration.html
- 