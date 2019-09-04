.. _percona-release:

================================================================================
Configuring Percona Repositories with percona-release 
================================================================================

The ``percona-release`` configuration tool allows users to automatically
configure which Percona repositories are enabled and disabled.

Installation
================================================================================

``percona-release`` can be installed with ``apt`` (for Debian and Ubuntu) or
``yum`` (for Red Hat Enterprise Linux and derivatives) package managers.

.. _percona-release.apt.installing:

DEB-Based GNU/Linux Distributions
--------------------------------------------------------------------------------

If you are running a DEB-based distribution, such as Debian or Ubuntu,
use the :command:`apt` package manager to install the ``percona-release``
official package:

.. admonition:: Prerequisites

   Running ``dpkg`` further in this procedure may fail due to unsatisfied
   dependencies that ``dpkg`` will not resolve for you.

   .. code-block:: text

      dpkg: error processing package percona-release (--install):
      installed percona-release package post-installation script subprocess returned error exit status 255

   In Linux distributions that rely on ``dpkg`` the packages ``wget``,
   ``gnupg2``, and ``lsb-release`` are already installed. However, these
   packages may be missing from Docker base images. In this case, install them
   manually *before running dpkg*:

   .. code-block:: bash

      $ sudo apt-get update
      $ sudo apt-get install -y wget gnupg2 lsb-release

1. Fetch the repository package:

   .. code-block:: bash
             
      $ wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb

#. Install the downloaded repository package with ``dpkg``:

   .. code-block:: bash
		   
      $ sudo dpkg -i percona-release_latest.generic_all.deb

   .. note::

      If ``dpkg`` fails at this step due to missing dependencies, run ``apt`` as follows:

      .. code-block:: bash

	 $ sudo apt install --fix-broken

#. Once you install this package the |Percona| repositories should be available. You
   can check the repository setup in the
   :file:`/etc/apt/sources.list.d/percona-release.list` file.


With ``percona-release`` package installed, :ref:`run the percona-release command <percona-release.usage>` to
set up the repository that contains the Percona product that you intend to
install.

.. seealso::

   Installing on Debian or Ubuntu:
      - `Percona Server for MySQL with the apt package manager <https://www.percona.com/doc/percona-server/LATEST/installation/apt_repo.html>`_
      - `Percona Server for MongoDB with the apt package manager <https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/apt.html>`_
      - `Percona XtraDB Cluster with the apt package manager <https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/apt.html>`_
      - `Percona XtraBackup with the apt package manager <https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/apt_repo.html>`_

.. _percona-release.rpm.installing:

RPM-Based GNU/Linux Distributions
--------------------------------------------------------------------------------

If you are running a RPM-based distribution, such as Red Hat Enterprise
Linux or CentOS, use the ``yum`` package manager, by running the following
command as the ``root`` user or with ``sudo``:

.. code-block:: bash

   $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

With ``percona-release`` package installed, :ref:`run the percona-release command <percona-release.usage>` to set up the repository that contains the
Percona product that you intend to install.

.. seealso::

   Installing on Red Hat and CentOS:
      - `Percona Server for MySQL with the yum package manager <https://www.percona.com/doc/percona-server/LATEST/installation/yum_repo.html>`_
      - `Percona Server for MongoDB with the yum package manager <https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/yum.html>`_
      - `Percona XtraDB Cluster with the yum package manager <https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/yum.html>`_
      - `Percona XtraBackup with the yum package manager <https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/yum_repo.html>`_

.. _percona-release.usage:

Usage
================================================================================

``percona-release`` has the following syntax:

.. code-block:: bash

   $ sudo percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]

Commands
--------------------------------------------------------------------------------

Available commands are ``enable``, ``enable-only``, ``disable``, and ``setup``:

* :option:`enable` command turns on an additional Percona *repository location*.
  For example, the following command enables the ``ps-80 release`` repository
  location:

  .. code-block:: bash

     $ sudo percona-release enable ps-80 release

* :option:`enable-only` command turns off all Percona repository locations, and
  enables the listed repository location after that. The following example first
  disables all Percona repository locations and then enables ``psmdb-40
  experimental``:

  .. code-block:: bash

     $ sudo percona-release enable-only psmdb-40 experimental

* :option:`disable` disables the specified repositories (or just ``all`` of them).
  For example, following command will disable all repository locations:

  .. code-block:: bash

     $ sudo percona-release disable all

* :option:`setup` :option:`<PRODUCT>` command  disables all current Percona
  repository locations, then enables the correct release repositories given a
  *product use*, and updates the platform's package manager database.
  :option:`<PRODUCT>` is the only parameter of this command, and it can be
  chosen from the following list: ``ps56``, ``ps57``, ``ps80``, ``psmdb34``,
  ``psmdb36``, ``psmdb40``, ``pxb80``, ``pxc56``, ``pxc57``, ``pxc80`` (the
  names are self explanatory). Following example will disable all Percona
  repository locations and then enable the ``release`` repository for *Percona
  Server for MySQL* 8.0:

  .. code-block:: bash

     $ percona-release setup ps80

Repository locations
--------------------------------------------------------------------------------

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

   $ sudo percona-release enable ps80 testing

This example enables installing a pre-release version of Percona Server for MySQL 8.0.

More examples: All steps for installing a specific Percona product 
================================================================================

.. rubric:: Percona XtraDB Cluster 8.0 on CentOS 7:

.. code-block:: bash

   $ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
   $ sudo percona-release enable-only pxc-80 release
   $ sudo percona-release enable tools-release
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

.. include:: .res/replace.program.txt

