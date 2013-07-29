# A Better Init script for Memcached

## Introduction

This is an init script for [memcached](http://www.memcached.org/) that allows to run
multiple instances of memcached based on configurations under `/etc/sysconfig`.

This script should run on any LSB-compliant environments while the original script is intended for Debian/Ubuntu only.

## Multiple server layout

Now it's easy to implement a multiserver setup. Just copy each file to
a file named:
    
    /etc/sysconfig/memcached-server1
    /etc/sysconfig/memcached-server2
            .
            .
            .
    /etc/sysconfig/memcached-serverN
   
Now you can either start/stop/restart all of your servers with a
single command like, for example:

    service memcached start 

Or start/stop/restart a specific server, for example server 3, like
this:

    service memcached start server3

Of course the numeric naming of the files is a mere convenience you
can **name** them as you wish as long as you maintain the pattern of
the dash for separating the server name. For example, server 2
works caching [drupal](http://drupal.org) menus. Providing a service
before provided by the `cache_menu` database table. You could name the
specific memcached server like this:

    memcached-server-cache_menu.conf

for example.

## Installation (confirmed on CentOS 6.4)

 1. Clone the repo 
    
        git clone git://github.com/yuryu/memcached-better-init-script.git

 2. Copy your memcached configuration file(s) under `/etc/sysconfig` to `/etc/sysconfig/memcached-server1`, `/etc/sysconfig/memcached-server2`, etc.
 
 3. Copy this script to `/etc/init.d`.
 
 4. Issue `service memcached force-reload`
 
 5. Done.


## Credits

The original init script is part of the debian testing distribution
[`wheezy`](http://packages.debian.org/wheezy/memcached). YMMV on other distrubutions.
