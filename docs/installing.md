# Installation


It is recommended to install Percona software
using the corresponding package manager for your system:


* **apt** for [Debian and Ubuntu](#install-on-debian-and-ubuntu)


* **yum** for [Red Hat Enterprise Linux and derivatives
(including CentOS, Oracle Linux, Amazon Linux AMI, etc.)](#install-on-red-hat-enterprise-linux-and-centos)

Find information about supported platforms on the [Percona Release Lifecycle Overview](https://www.percona.com/services/policies/percona-software-support-lifecycle#support).

### Install on Debian and Ubuntu

If you are running a DEB-based distribution, such as Debian or Ubuntu,
use the **apt** package manager to install the `percona-release`
official package:

!!! admonition "Prerequisites"

    In Linux distributions that rely on `dpkg`, the packages `wget`, `gnupg2`, `curl` and `lsb-release` are already installed. However, these packages may be missing from Docker base images. In this case, install them manually before running `dpkg`:

    ```
    sudo apt update
    sudo apt install -y wget gnupg2 curl lsb-release 
    ```


1. Fetch the repository package:

    ```
    wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
    ```


2. Install the downloaded repository package with `dpkg`:

    ```
    sudo dpkg -i percona-release_latest.generic_all.deb
    ```


3. After installation, the *Percona* repositories are available. You
can check the repository setup for the Percona original release list in the
`/etc/apt/sources.list.d/percona-original-release.list` file.

    !!! note
   
        If you have enabled another repository, the file name is different.


4. Refresh the local cache to update the package information:

    ```
    sudo apt update
    ```

!!! admonition "Dealing with issues"

    During the installation, `dpkg` may fail due to unsatisfied dependencies.

    ```
    dpkg: error processing package percona-release (--install):
    installed percona-release package post-installation script subprocess returned error exit status 255
    ```

    In this case, run the following command:

    ```
    sudo apt install --fix-broken
    ```

> **Next steps**:  run the ``percona-release`` command to
[set up the repository](#usage) that contains the Percona product that you intend to install.

!!! seeaslso

    Debian and Ubuntu with the apt package manager:

    * [Percona Server for MySQL](https://www.percona.com/doc/percona-server/LATEST/installation/apt_repo.html)
    * [Percona Server for MongoDB](https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/apt.html)
    * [Percona XtraDB Cluster](https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/apt.html)
    * [Percona XtraBackup](https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/apt_repo.html)
    * [Percona Distribution for PostgreSQL](https://www.percona.com/doc/postgresql/LATEST/installing.html#on-debian-and-ubuntu-using-apt)
    * [Percona Distribution for MongoDB](https://www.percona.com/doc/percona-distribution-for-mongodb/LATEST/installation.html#install-on-debian-ubuntu)
    * [Percona Distribution for MySQL](https://www.percona.com/doc/percona-distribution-mysql/8.0/installing.html#install-pdmysql)

### Install on Red Hat Enterprise Linux and CentOS

If you are running an RPM-based distribution, such as Red Hat Enterprise
Linux or CentOS, use the `yum` package manager to install `percona-release`. Run the following command as the `root` user or with `sudo`:

```
$ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
```

> **Next steps**:  run the ``percona-release`` command to
[set up the repository](#usage) that contains the Percona product that you intend to install.

!!! seeaslso

    Red Hat and CentOS with the yum package manager:

    * [Percona Server for MySQL](https://www.percona.com/doc/percona-server/LATEST/installation/yum_repo.html)
    * [Percona Server for MongoDB](https://www.percona.com/doc/percona-server-for-mongodb/LATEST/install/yum.html)
    * [Percona XtraDB Cluster](https://www.percona.com/doc/percona-xtradb-cluster/LATEST/install/yum.html)
    * [Percona XtraBackup](https://www.percona.com/doc/percona-xtrabackup/LATEST/installation/yum_repo.html)
    * [Percona Distribution for PostgreSQL](https://www.percona.com/doc/postgresql/LATEST/installing.html#on-red-hat-enterprise-linux-and-centos-using-yum)
    * [Percona Distribution for MongoDB](https://www.percona.com/doc/percona-distribution-for-mongodb/LATEST/installation.html#install-on-red-hat-enterprise-linux-centos)
    * [Percona Distribution for MySQL](https://www.percona.com/doc/percona-distribution-mysql/8.0/installing.html#install-pdmysql) 
