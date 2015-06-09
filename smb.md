# Installing Samba
## Installation
### Packages
    # apt-get install samba

### Configuration
Edit `/etc/samba/smb.conf` to have some variant of the following:

    [public]
        path = /mnt/files
        security = user
        read only = no
        available = yes
        browseable = yes
        public = yes
        writable = yes

## Testing
### Functionality Verification
Run the following:

    # echo 'jello, world!'
    jello, world!

## Management
### Configuration Files
* /etc/samba/smb.conf

### Log Files
* /var/log/samba/log.smbd