Graphite Installation
===

OS Packages
---

#) As always:

    $ apt-get update

#) Install packages:

    $ apt-get install python-pip python-cairo python-django python-django-tagging libapache2-mod-wsgi python-twisted python-memcache python-pysqlite2 python-simplejson memcached sqlite3 libsqlite3-dev

Software Installation
---

#) Install via pip:

    $ pip install whisper carbon graphite-web

#) Set configuration files in ``/opt/graphite/conf/``:

    $ cd /opt/graphite/conf/

    $ cp graphite.wsgi.example graphite.wsgi

    $ cp carbon.conf.example carbon.conf

    $ cp storage-schemas.conf.example storage-schemas.conf

#) Edit ``storage-schemas.conf`` to contain the following tweaks (replace 'stats' with your global prefix):

    [stats]
    pattern = ^stats.*
    retentions = 10s:6h,1min:7d,10min:5y

#) Set configuration files ``/opt/graphite/webapp/graphite``:

    $ cd /opt/graphite/webapp/graphite

    $ cp local_settings.py.example local_settings.py

#) Edit ``local_settings.py`` to have the correct values for ``MEMCACHE_HOSTS``, ``TIME_ZONE``, and ``DATABASES``

#) Create the ``storage-aggregation.conf`` file from our template:

    $ cp ./graphite/storage-aggregation.conf.example /opt/graphite/conf/storage-aggregation.conf

#) Initialize graphite's DB:

    $ cd /opt/graphite/webapp/graphite

    $ python manage.py syncdb

    $ chown -R www-data:www-data /opt/graphite/storage

#) WHERE necessary, create an apache2 website for graphite:

    $ cp ./graphite/vhost.conf /etc/apache2/sites-available/graphite

    $ a2ensite graphite

    $ service apache2 restart

Software Verification
---

### Testing the graphite browser

#) Testing for success:

    $ curl graphite.domain.tld | grep -i "Graphite Browser"

        <title>Graphite Browser</title>

### Software verification cleanup

    $ a2dissite graphite

    $ service apache2 restart

    $ rm /etc/apache2/sites-available/graphite

Log Files
---

* /opt/graphite/storage/log/webapp/access.log

* /opt/graphite/storage/log/webapp/error.log

* /opt/graphite/storage/log/webapp/info.log

* /opt/graphite/storage/log/webapp/exception.log