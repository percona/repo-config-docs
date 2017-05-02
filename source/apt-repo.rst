.. _apt-repo:

===================================================
Configuring Percona Repository on Debian and Ubuntu
===================================================

If you are running a DEB-based Linux distribution,
use the :command:`apt` package manager to install Percona software
from the official repository.

1. Fetch the repository package::

    wget https://repo.percona.com/apt/percona-release_0.1-4.$(lsb_release -sc)_all.deb

#. Install the repository package::

    sudo dpkg -i percona-release_0.1-4.$(lsb_release -sc)_all.deb

#. Update local :command:`apt` cache::

    sudo apt-get update

#. Make sure that Percona packages are available::

    sudo apt-cache search percona

   You should see output similar to the following::

    percona-xtrabackup-dbg - Debug symbols for Percona XtraBackup
    percona-xtrabackup-test - Test suite for Percona XtraBackup
    percona-xtradb-cluster-client - Percona XtraDB Cluster database client
    percona-xtradb-cluster-server - Percona XtraDB Cluster database server
    percona-xtradb-cluster-testsuite - Percona XtraDB Cluster database regression test suite
    percona-xtradb-cluster-testsuite-5.5 - Percona Server database test suite
    ...

