inkscope-packaging
==================

packaging tools for inkscope
----------------------------

The RPMS directory  contains all  inkscope  rpms and  dependancy, and also deb packages.

        inkscope-sysprobe :  installs  probes on  all servers with osd and mons
        inkscope-cephrestapi:  installs  all file to  start a ceph rest api
        inkscope-cephprobe: installs the cephprobe ( only one is  needed for all the cluster)
        inkscope-admviz : installs  inskcope web interface
        inkscope-common :  contains all configuration files for probes and  admin interface.

You need to  install a mongodb database and  instanciate /opt/inkscope/etc/inkscope.conf file. You can use chef or puppet to do this.

A version of python-psutils greater than 2.0  is needed

Install it on Debian compliant os:
=================================

see on Inkscope blog : http://inkscope.blogspot.fr/2015/12/inkscope-v13-installation-on-debian.html


Install it on a redhat compliant os:
====================================
Create a directory for you local repository, e.g. /home/user/inkscope_repo.
Move the RPMs into that directory.
Fix some ownership and filesystem permissions:

    chown -R root.root /home/user/inkscope_repo
    
Install the createrepo package if not installed yet, and run

    createrepo /home/user/repo
    chmod -R o-w+r /home/user/repo

Create a repository configuration file, e.g. /etc/yum.repos.d/inkscope_repo.repo containing

    [local]
    name=My inkScope Repo
    baseurl=file:///home/user/inkscope_repo
    enabled=1
    gpgcheck=0


install cephprobe and ceph-rest-api
-----------------------------------

on a server SRVAPI:

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
