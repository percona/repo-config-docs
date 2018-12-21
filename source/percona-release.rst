.. _percona-release:

=====================================================================
Configuring Percona Repositories with percona-release 
=====================================================================

The ``percona-release`` configuration tool allows users to automatically
configure which Percona repositories are enabled and disabled.

Installation
============

``percona-release`` can be installed with ``apt`` (for Debian and Ubuntu) or
``yum`` (for Red Hat Enterprise Linux and derivatives) package managers.

Install on DEB-Based GNU/Linux Distribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are running a DEB-based distribution, such as Debian or Ubuntu,
use the :command:`apt` package manager to install the ``percona-release``
official package:

1. Fetch the repository package::

      $ wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb

#. Install the downloaded repository package with ``dpkg``::

   # dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb

Install on RPM-Based GNU/Linux Distribution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are running some RPM-based distribution, such as Red Hat Enterprise
Linux and CentOS, use the ``yum`` package manager, by running the following
command as the ``root`` user or with ``sudo``::

   # yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

Usage
=====

``percona-release`` accepts the following command line arguments::

   percona-release.sh <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]

Commands
--------

Available commands are ``enable``, ``enable-only``, ``disable``, and ``setup``:

* :option:`enable` command turns on an additional Percona *repository location*.
  For example, following command will enable the ``ps-80 release`` repository
  location::

    # percona-release enable ps-80 release

* :option:`enable-only` command turns off all Percona repository locations, and
  enables the listed repository location after that. Following example will
  first disable all Percona repository locations and then enable the
  ``psmdb-40 experimental`` one::

    # percona-release enable-only psmdb-40 experimental

* :option:`disable` disables the specified repositories (or just ``all`` of them).
  For example, following command will disable all repository locations::

    # percona-release disable all

* :option:`setup` :option:`<PRODUCT>` command  disables all current Percona
  repository locations, then enables the correct release repositories given a
  *product use*, and updates the platform's package manager database.
  :option:`<PRODUCT>` is the only parameter of this command, and it can be
  chosen from the following list: ``ps56``, ``ps57``, ``ps80``, ``psmdb34``,
  ``psmdb36``, ``psmdb40``, ``pxb80``, ``pxc56``, ``pxc57``, ``pxc80`` (the
  names are self explanatory). Following example will disable all Percona
  repository locations and then enable the ``release`` repository for *Percona
  Server for MySQL* 8.0::

    # percona-release setup ps80

Repository locations
--------------------

*Repository location* may contain two parts: a *repository* and a *component*.
Available repositories are ``original``, ``ps-80``, ``pxc-80``, ``psmdb-40``,
and ``tools``.

* ``original`` repository is the place to get Percona’s products of the previous
  versions which haven’t yet reach their end of life and are still supported,
  such as *Percona Server for MySQL* 5.6 and 5.7, *Percona XtraDB Cluster* 5.6
  and 5.7, *Percona Server for MongoDB* 3.4 and 3.6, etc.
* ``ps-80`` repository hosts packages for *Percona Server for MySQL* 8.0.
* ``pxc-80`` repository is for *Percona XtraDB Cluster* 8.0 packages.
* ``psmdb-40`` repository is hosting *Percona Server for MongoDB* 4.0
  packages.
* ``tools`` repository hosts all other products and tools: *Percona XtraBackup*
  8.0, *Percona Toolkit*, *PMM Client*,  *ProxySQL*, etc.

Available components are ``release`` (used by default), ``testing``, and
``experimental``.

* ``release`` stores released GA packages of products through *Percona Server
  for MySQL* 5.7 and *Percona Server for MongoDB* 3.6 based products along with
  other tools.
* ``testing`` is used for final QA and package testing for GA candidate packages
  of products.
* ``experimental`` hosts alpha/beta releases of products.

For example, to prepare a system for installation of *Percona Server for
MySQL* 8.0, user should execute the
following command after installation of the ``percona-release`` tool::

  # percona-repo enable-only ps-80 release

More examples
=============

1. The following example contains commands which will install *Percona XtraDB
   Cluster* 8.0 on CentOS 7::

      $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
      $ sudo percona-release enable-only pxc-80 release
      $ sudo percona-release enable tools-release
      $ sudo yum install percona-xtradb-cluster

#. The following example is helpful if you want to install *Percona Server for
   MySQL* 8.0, *Percona Toolkit*, *Percona XtraBackup* and *Sysbench* the on
   Ubuntu 18.04::

      $ wget wget https://repo.percona.com/apt/percona-release_latest.bionic_all.deb
      $ sudo dpkg -i percona-release_1.0-1.bionic_all.deb
      $ sudo percona-release enable-only ps-80 release
      $ sudo percona-release enable tools release
      $ sudo apt-get update
      $ sudo apt-get install percona-server-server percona-server-client percona-toolkit percona-xtrabackup-80 sysbench

#. The following example will install the *Percona Server for MySQL* 8.0 release
   package on CentOS and other RPM-based systems::

      $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
      $ sudo percona-release setup ps80
      $ sudo yum install percona-server-server

#. The following example will install the *Percona Server for MongoDB* 3.6
   release package on Ubuntu or some other DEB-based GNU/Linux distribution::

      $ wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb
      $ sudo dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb
      $ sudo percona-release setup psmdb36
      $ sudo apt-get install percona-server-mongodb-36






