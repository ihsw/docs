# Installing Php and Php-Fpm
## Installation
### Packages
    # apt-get install php5 php5-cli php5-fpm php5-mysqlnd

### Configuration
Edit the `php.ini` configs to have some variant of the following values:

    date.timezone = America/Montreal
    cgi.fix_pathinfo=0

## Testing
### Functionality Verification
Run the following:

    # php --version

    PHP 5.5.3 (cli) (built: Aug 31 2013 21:12:56) 
    Copyright (c) 1997-2013 The PHP Group
    Zend Engine v2.5.0, Copyright (c) 1998-2013 Zend Technologies

    # php5-fpm --version

    PHP 5.5.3 (fpm-fcgi) (built: Aug 31 2013 21:13:10)
    Copyright (c) 1997-2013 The PHP Group
    Zend Engine v2.5.0, Copyright (c) 1998-2013 Zend Technologies

## Management
### Configuration Files
* /etc/php5/cli/php.ini
* /etc/php5/fpm/php.ini

### Log Files
* /var/log/php5-fpm.log