inkscope-packaging
==================

packaging tools for inkscope
----------------------------

The RPMS directory  contains all  inkscope  rpms and  dependancy, and also deb packages.

        inkscope-sysprobe :  installs  probes on  all servers with osd and mons
        inkscope-cephrestapi:  installs  all file to  start a ceph rest api
        inkscope-cephprobe: installs the cephprobe ( only one is  needed for all the cluster)
        inkscope-admviz : installs  inskcope insterface
        inkscope-common :  contains all configuration files for probes and  admin interface.

You need to  install a mongodb database and  instanciate /opt/inkscope/etc/inkscope.conf file. You can use chef or puppet to do this.

A version of python-psutils greater than 2.0  is needed

Install it on Debian compliant os:
=================================
Add the  repository in your source list:
    
    vi /etc/apt/sources.list.d/inkscope.list

    deb https://raw.githubusercontent.com/inskscope/inkscope-packaging/master/DEBS ./

    apt-get update

install cephprobe
-----------------
on a server with a mon:
    
    sudo apt-get install inkscope-cephrestapi
    /etc/init.d/cephrestapi start
    sudo apt-get inkscope-cephprobe
    /etc/init.d/cephprobe start

install sysprobe
----------------

on each server:

    sudo apt-get install inkscope-sysprobe
    edit  /opt/inkscope/etc/inkscope.conf
    /etc/init.d/sysprobe start


install inskscopeviz
--------------------

on a  server SRVVIZ :

    sudo apt-get install inkscope-admviz
    edit  /opt/inkscope/etc/inkscope.conf
    edit  /etc/apache2/conf.d/inkScope.conf
    edit /etc/apache2/ports.conf
        
        Listen 8080

    enable proxy module

        sudo a2enmod proxy_http

    enable inkscope
        sudo a2ensite inkScope

    restart apache
        sudo service apache2 restart

    http://SRVVIZ:8080/inkscopeViz


Install it on a redhat compliant os:
====================================

install cephprobe
-----------------

on a server with a mon:

    yum install inkscope-cephrestapi
    /etc/init.d/cephrestapi start
    yum install inkscope-cephprobe
    edit  /opt/inkscope/etc/inkscope.conf
    /etc/init.d/cephprobe start
    

     
install sysprobe
----------------
     
on each server:

    yum install inkscope-sysprobe
    edit  /opt/inkscope/etc/inkscope.conf
    /etc/init.d/sysprobe start


install inskscopeviz
----------------------------

on a  server SRVVIZ :

    yum install inkscope-admviz
    edit  /opt/inkscope/etc/inkscope.conf
    edit  /etc/httpd/conf.d/inkScope.conf
    systemctl start httpd
    http://SRVVIZ:8080/inkscopeViz

How to update
-------------

     yum update package

if the following  config file exists it keeps the original one.
    /etc/httpd/conf.d/inkScope.conf
    /opt/inkscope/etc/inkscope.conf
