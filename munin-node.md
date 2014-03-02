# Installing Munin
## Installation
### Packages
    # apt-get install munin-node munin-plugins-extra

### Configuration
Edit `/etc/munin/munin-node.conf` to have some variant of the following:

    hostname node01
    allow ^192.68.1.3$

Where `192.168.1.3` points to the server that this node belongs to.

## Testing
### Functionality Verification
#### Connectivity

Running:

    # nc 192.168.1.2 4949

Should result in:

    # munin node at node01

Where you can now enter:

    fetch df

Should result in:

    rootfs.value 15.524721378347
    [...]

## Management
### Configuration Files
* /etc/munin/munin-node.conf

### Log Files
* /var/log/munin/munin-node.log