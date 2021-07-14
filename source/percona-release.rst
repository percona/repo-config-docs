.. _percona-release:

================================================================================
Configuring Percona Repositories with percona-release 
================================================================================

.. raw:: html

   <style>
   
   .toggle {
        background: none repeat scroll 0 0 #f5f5f5;
        padding: 12px;
        max-width: 850px;
        line-height: 24px;
        margin-bottom: 24px;
    }
   
   .toggle .header {
       display: block;
       clear: both;
       cursor: pointer;
   }
   
   .toggle .header:after {
       content: " ▶";
   }
   
   .toggle .header.open:after {
       content: " ▼";
   }
   </style>


The |percona-release| configuration tool allows users to automatically
configure which Percona repositories are enabled and disabled.

.. contents::
   :local:

Installation
================================================================================

``percona-release`` can be installed with ``apt`` (for Debian and Ubuntu) or
``yum`` (for Red Hat Enterprise Linux and derivatives) package managers. Find information about supported platforms on the `Percona Release Lifecycle Overview <https://www.percona.com/services/policies/percona-software-support-lifecycle#support>`_.

.. _percona-release.apt.installing:

Debian and Ubuntu 
--------------------------------------------------------------------------------

If you are running a DEB-based distribution, such as Debian or Ubuntu,
use the :command:`apt` package manager to install the ``percona-release``
official package:

.. admonition:: Prerequisites

   In Linux distributions that rely on ``dpkg``, the packages ``wget``,
   ``gnupg2``, ``curl`` and ``lsb-release`` are already installed. However, these
   packages may be missing from Docker base images. In this case, install them
   manually *before running dpkg*:

   .. code-block:: bash

      $ sudo apt-get update
      $ sudo apt-get install -y wget gnupg2 lsb-release curl

1. Fetch the repository package:

   .. code-block:: bash
             
      $ wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb

#. Install the downloaded repository package with ``dpkg``:

   .. code-block:: bash
		   
      $ sudo dpkg -i percona-release_latest.generic_all.deb

#. After installation, the |Percona| repositories are available. You
   can check the repository setup for the Percona original release list in the
   :file:`/etc/apt/sources.list.d/percona-original-release.list` file.

   .. note::

      If you have enabled another repository, the file name is different.

#. Refresh the local cache to update the package information:
   
   .. code-block:: bash
   
      $ sudo apt-get update

.. note::

   During the installation, ``dpkg`` may fail due to unsatisfied
   dependencies.

   .. code-block:: text

      dpkg: error processing package percona-release (--install):
      installed percona-release package post-installation script subprocess returned error exit status 255

   In this case, run the following command:

   .. code-block:: bash
   
      $ sudo apt-get install --fix-broken

With ``percona-release`` package installed, :ref:`run the percona-release command <percona-release.usage>` to
set up the repository that contains the Percona product that you intend to
install.

.. seealso::

   Debian or Ubuntu with the apt package manager:
      - `Percona Server for MySQL <https://www.percona.com/doc/percona-server/LATEST/installation/apt_repo.html>`_
      - `Percona Server for MongoDB  <https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/apt.html>`_
      - `Percona XtraDB Cluster  <https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/apt.html>`_
      - `Percona XtraBackup  <https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/apt_repo.html>`_
      - `Percona Distribution for PostgreSQL  <https://www.percona.com/doc/postgresql/LATEST/installing.html#using-the-deb-format>`_
      - `Percona Distribution for MongoDB <https://www.percona.com/doc/percona-distribution-for-mongodb/LATEST/installation.html#install-on-debian-ubuntu>`_
      - `Percona Distribution for MySQL
	<https://www.percona.com/doc/percona-distribution-mysql/8.0/installing.html#install-pdmysql>`_
	
.. _percona-release.rpm.installing:

Red Hat Enterprise Linux and CentOS
--------------------------------------------------------------------------------

If you are running a RPM-based distribution, such as Red Hat Enterprise
Linux or CentOS, use the ``yum`` package manager, by running the following
command as the ``root`` user or with ``sudo``:

.. code-block:: bash

   $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

With ``percona-release`` package installed, :ref:`run the percona-release command <percona-release.usage>` to set up the repository that contains the
Percona product that you intend to install.

.. seealso::

   Red Hat and CentOS with the yum package manager:
      - `Percona Server for MySQL
	<https://www.percona.com/doc/percona-server/LATEST/installation/yum_repo.html>`_
      - `Percona Server for MongoDB
	<https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/yum.html>`_
      - `Percona XtraDB Cluster
	<https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/yum.html>`_
      - `Percona XtraBackup
	<https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/yum_repo.html>`_
      - `Percona Distribution for PostgreSQL
	<https://www.percona.com/doc/postgresql/LATEST/installing.html#using-the-rpm-format>`_
      - `Percona Distribution for MongoDB
	<https://www.percona.com/doc/percona-distribution-for-mongodb/LATEST/installation.html#install-on-red-hat-enterprise-linux-centos>`_
      - `Percona Distribution for MySQL
	<https://www.percona.com/doc/percona-distribution-mysql/8.0/installing.html#install-pdmysql>`_

.. _percona-release.usage:

Usage
================================================================================

``percona-release`` has the following syntax:

.. code-block:: bash

   $ sudo percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]

Commands
--------------------------------------------------------------------------------

Available commands are ``enable``, ``enable-only``, ``disable``, ``setup`` and ``show``:

* ``show`` command shows the enabled repositories in your system:

  .. code-block:: bash
  
     $ sudo percona-release show

  .. admonition:: Sample output
  
     .. code-block:: text

        The following repos are enabled on your system:
        http://repo.percona.com/percona/apt
        http://repo.percona.com/prel/apt  

* ``enable`` command turns on an additional Percona *repository location*.
  For example, the following command enables the ``ps-80 release`` repository
  location:

  .. code-block:: bash

     $ sudo percona-release enable ps-80 release

* ``enable-only`` command turns off all Percona repository locations, and
  enables the listed repository location after that. The following example first
  disables all Percona repository locations and then enables ``psmdb-40
  experimental``:

  .. code-block:: bash

     $ sudo percona-release enable-only psmdb-40 experimental

* ``disable`` disables the specified repositories (or just ``all`` of them).
  For example, following command will disable all repository locations:

  .. code-block:: bash

     $ sudo percona-release disable all

  .. note:: 

     The ``prel`` repository remains enabled. This repository stores the ``percona-release`` packages and is always enabled for ``percona-release`` to operate.

* ``setup`` `<PRODUCT>` command disables all current Percona
  repository locations, then enables the correct release repositories given a
  *product use*, and updates the platform's package manager database.
  `<PRODUCT>` is the only parameter of this command, and it can be
  chosen from the following list (the names of products are self-explanatory):

  .. hlist::
     :columns: 3

     - ``ps56``
     - ``ps57``
     - ``ps80``
     - ``psmdb34``
     - ``psmdb36``
     - ``psmdb40``
     - ``psmdb42``
     - ``psmdb44``
     - ``pxb24``
     - ``pxb80``
     - ``pxc56``
     - ``pxc57``
     - ``pxc80``
     - ``ppg11``
     - ``ppg11.5``
     - ``ppg11.6``
     - ``ppg11.7``
     - ``ppg11.8``
     - ``ppg11.9``
     - ``ppg11.10``
     - ``ppg11.11``
     - ``ppg11.12``
     - ``ppg12``
     - ``ppg12.2``
     - ``ppg12.3``
     - ``ppg12.4``
     - ``ppg12.5``
     - ``ppg12.6``
     - ``ppg12.7``
     - ``ppg13``
     - ``ppg13.0``
     - ``ppg13.1``
     - ``ppg13.2``
     - ``ppg13.3``
     - ``pdmdb4.2``
     - ``pdmdb4.2.6``
     - ``pdmdb4.2.7``
     - ``pdmdb4.2.8``
     - ``pdmdb4.2.9``
     - ``pdmdb4.2.10``
     - ``pdmdb4.2.11``
     - ``pdmdb4.2.12``
     - ``pdmdb4.2.13``
     - ``pdmdb4.2.14``
     - ``pdmdb4.4``
     - ``pdmdb4.4.0``
     - ``pdmdb4.4.1``
     - ``pdmdb4.4.2``
     - ``pdmdb4.4.3``
     - ``pdmdb4.4.4``
     - ``pdmdb4.4.5``
     - ``pdmdb4.4.6``
     - ``pdps8.0``
     - ``pdps8.0.19``
     - ``pdps8.0.20``
     - ``pdps8.0.21``
     - ``pdps8.0.22``
     - ``pdps8.0.23``
     - ``pdps8.0.25``
     - ``pdpxc8.0``
     - ``pdpxc8.0.19``
     - ``pdpxc8.0.20``
     - ``pdpxc8.0.21``
     - ``pdpxc8.0.22``
     - ``pdpxc8.0.23``
     - ``prel``
     - ``proxysql``
     - ``sysbench`` 
     - ``pt`` 
     - ``pmm-client``
     - ``pmm2-client`` 
     - ``mysql-shell`` 
     - ``pbm`` 

  The following example disables all Percona repository locations and then
  enables the ``release`` repository for *Percona Server for MySQL* 8.0. This
  command runs in the interactive mode and may request extra input from you,
  depending on your platform.

  .. code-block:: bash

     $ percona-release setup ps80

  In non-interactive contexts, such as in scripts, requests for extra input may
  halt the program.  Run the ``setup`` command with the `-y` option to provide
  the affirmative answer where input from the user would be requested in the
  interactive mode.

  .. code-block:: bash

     $ percona-release setup -y ps80

Repository locations
--------------------------------------------------------------------------------

*Repository location* may contain two parts: a *repository* and a *component*.
Available repositories are:

.. container:: toggle

   .. container:: header

      **MySQL Software**:

   .. include:: .res/mysql-repos.txt

.. container:: toggle

   .. container:: header

      **MongoDB Software**:

   .. include:: .res/mongodb-repos.txt

.. container:: toggle

   .. container:: header

      **PostgreSQL Software**:

   .. include:: .res/postgresql-repos.txt

.. container:: toggle

   .. container:: header

      **Percona Tools**:

   .. include:: .res/tools-repos.txt
            
Components
--------------------------------------------------------------------------------

By using a component you may choose to use either the GA version of the selected
product or its beta version. |percona-release| recognizes ``release`` (used by
default), ``testing``, and ``experimental`` components.

.. list-table::

   * - Component
     - Usage
   * - release
     - Stores released GA packages of products. 
   * - testing
     - Is used for final QA and package testing for GA candidate packages of products.
   * - experimental
     - Hosts alpha and beta releases of products

For example, to prepare your system for installation of *Percona Server for MySQL*
8.0, run ``percona-release`` as follows:

.. code-block:: bash
		
   $ sudo percona-release enable-only ps-80 release

To enable pre-release builds from the testing repository, run |percona-release|
with the ``testing`` component.

.. code-block:: bash

   $ sudo percona-release enable ps-80 testing

This example enables installing a pre-release version of Percona Server for MySQL 8.0.

Example: All steps for installing a specific Percona product 
================================================================================

.. rubric:: Percona XtraDB Cluster 8.0 on CentOS 7:

.. code-block:: bash

   $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
   $ sudo percona-release enable-only pxc-80 release
   $ sudo percona-release enable tools release
   $ sudo yum install percona-xtradb-cluster

.. rubric:: Percona Server for MySQL 8.0, Percona Toolkit, Percona XtraBackup and Sysbench on Ubuntu 18.04:

.. code-block:: bash

   $ wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
   $ sudo dpkg -i percona-release_latest.generic_all.deb
   $ sudo percona-release enable-only ps-80 release
   $ sudo percona-release enable tools release
   $ sudo apt-get update
   $ sudo apt-get install percona-server-server percona-server-client percona-toolkit percona-xtrabackup-80 sysbench

.. rubric:: Percona Server for MySQL 8.0 release package on CentOS or other RPM-based systems:

.. code-block:: bash

   $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
   $ sudo percona-release setup ps80
   $ sudo yum install percona-server-server

.. rubric:: Percona Server for MongoDB 3.6 release package on Ubuntu or another DEB-based GNU/Linux distribution:

.. code-block:: bash

   $ wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb 
   $ sudo dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb
   $ sudo percona-release setup psmdb36
   $ sudo apt-get install percona-server-mongodb-36

.. _percona-release-update-latest-version:

Updating |percona-release| to the Latest Version
================================================================================

|percona-release| itself is available from the *prel* repository which is enabled by default. Thus, to update |percona-release|, simply run the following command as root or via sudo:

- For RPM-based systems:

  .. code-block:: bash

     $ yum update percona-release

- For DEB-based systems:

  .. code-block:: bash

     #Update the local cache
     $ apt-get update
     #Update percona-release
     $ apt-get install percona-release

.. include:: .res/replace.program.txt

