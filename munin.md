# Installing Munin
## Installation
### Packages
    # apt-get install munin

### Configuration
Edit `/etc/munin/munin.conf` to have some variant of the following:

    [node01]
        address 192.168.1.2

Note: there is no munin service, only cronjobs. They will automatically pick up the new config.

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

#### Configuration Validity

Run:

	# su -s /bin/bash munin
    # /usr/share/munin/munin-update --debug --nofork --host node01 --service df

Should result in:

    2014/03/02 15:02:42 [DEBUG] Creating new lock file /var/run/munin/munin-update.lock
    2014/03/02 15:03:25 [DEBUG] Creating lock : /var/run/munin/munin-update.lock succeeded
    2014/03/02 15:03:25 [INFO]: Starting munin-update
    2014/03/02 15:03:25 [DEBUG] Creating new lock file /var/run/munin/munin-node01-node01.lock
    [...]

## Management
### Configuration Files
* /etc/munin/munin.conf

### Log Files
* /var/log/munin/munin-update.log