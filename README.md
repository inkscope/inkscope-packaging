inkscope-packaging
==================

packaging tools for inkscope
----------------------------

The RPMS directory  contains all  inkscope  rpms and  dependancy.

        inkscope-sysprobe :  installs  probes on  all servers with osd and mons
        inkscope-cephrestapi:  installs  all file to  start a ceph rest api
        inkscope-cephprobe: installs the cephprobe ( only one is  needed for all the cluster)
        inkscope-admviz : installs  inskcope insterface
        inkscope-common :  contains all configuration files for probes and  admin interface.

You need to  install a mongodb database and  instanciate /opt/inkscope/etc/inkscope.conf file. You can use chef or puppet to do this.
   
How to install cephprobe
------------------------

on a server with a mon:

    yum install inkscope-cephrestapi
    /etc/init.d/cephrestapi start
    yum install inkscope-cephprobe
    edit  /opt/inkscope/etc/inkscope.conf
    /etc/init.d/cephprobe start
    
     
How to install sysprobe
-----------------------
     
on each server:

    yum install inkscope-sysprobe
    edit  /opt/inkscope/etc/inkscope.conf
    /etc/init.d/sysprobe start


How to  install inskscopeviz
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
