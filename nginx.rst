Installation
============

Packages
--------

#) Install as such:

    # apt-get install nginx

    # service nginx start

Nginx doesn't usually start after installation.

Configuration
-------------

#) Edit ``/etc/nginx/sites-enabled/default`` to have some variant of the following location blocks:

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }

Where `fastcgi_pass` leads to either a unix or tcp socket, preferably unix socket for double-plus good security.

Testing
=======

Functionality Verification
--------------------------

#) Run the following command:

    # curl -s localhost | grep -i 'welcome to nginx'

    <title>Welcome to nginx!</title>

    <center><h1>Welcome to nginx!</h1></center>

Management
==========

Configuration Files
-------------------

* /etc/nginx/nginx.conf

Log Files
---------

* /var/log/nginx/access.log

* /var/log/nginx/error.log