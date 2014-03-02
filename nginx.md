# Installing Nginx
## Installation
### Packages
    # apt-get install nginx
    # service nginx start
Nginx doesn't start after installation.

### Configuration
#### General
Edit `/etc/nginx/sites-enabled/default` to have some variant of the following location blocks:

    location / {
        try_files $uri $uri/ =404;
    }

#### PHP
    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }

Where `fastcgi_pass` leads to either a unix or tcp socket, preferably unix socket for double-plus good security.

#### Munin
Furthermore have this above anything else:

    location /munin/static/ {
        alias /etc/munin/static/;
        expires modified +1w;
    }   

    location /munin/ {
        # auth_basic            "Restricted";
        # Create the htpasswd file with the htpasswd tool.
        # auth_basic_user_file  /etc/nginx/htpasswd;

        alias /var/cache/munin/www/;
        expires modified +310s;
    }

## Testing
### Functionality Verification
Run the following:

    # curl -s localhost | grep -i 'welcome to nginx'
    <title>Welcome to nginx!</title>
    <center><h1>Welcome to nginx!</h1></center>

## Management
### Configuration Files
* /etc/nginx/nginx.conf

### Log Files
* /var/log/nginx/access.log
* /var/log/nginx/error.log