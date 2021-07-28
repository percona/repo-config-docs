# Configuring Percona Repositories with percona-release

The **percona-release** configuration tool allows users to automatically
configure which Percona repositories are enabled and disabled.

* [Installation](#installation)
* [Usage](#usage)
* [Examples](#examples-all-steps-for-installing-a-specific-percona-product)
* [Updating percona-release to the latest version](#updating-percona-release-to-the-latest-version)

## Installation

You can install `percona-release` with the package manager of your operating system. Use the following instructions:

* [Install on Debian and Ubuntu](#install-on-debian-and-ubuntu) 
* [Install on Red Hat Enterprise Linux and CentOS](#install-on-red-hat-enterpise-linux-and-centos).

Find information about supported platforms on the [Percona Release Lifecycle Overview](https://www.percona.com/services/policies/percona-software-support-lifecycle#support).

### Install on Debian and Ubuntu

If you are running a DEB-based distribution, such as Debian or Ubuntu,
use the **apt** package manager to install the `percona-release`
official package:

!!! admonition "Prerequisites"

    In Linux distributions that rely on `dpkg`, the packages `wget`, `gnupg2`, `curl` and `lsb-release` are already installed. However, these packages may be missing from Docker base images. In this case, install them manually before running `dpkg`:

    ```
    sudo apt-get update
    sudo apt-get install -y wget gnupg2 curl lsb-release 
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
    sudo apt-get update
    ```

!!! admonition "Dealing with issues"

    During the installation, `dpkg` may fail due to unsatisfied dependencies.

    ```
    dpkg: error processing package percona-release (--install):
    installed percona-release package post-installation script subprocess returned error exit status 255
    ```

    In this case, run the following command:

    ```
    sudo apt-get install --fix-broken
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

## Usage

`percona-release` has the following syntax:

```
$ sudo percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]
```

### Commands

Available commands are `enable`, `enable-only`, `disable`, `setup` and `show`:


* `show` command shows the enabled repositories in your system:

```
sudo percona-release show
```


* `enable` command turns on an additional Percona *repository location*.
For example, the following command enables the `ps-80 release` repository
location:

```
$ sudo percona-release enable ps-80 release
```


* `enable-only` command turns off all Percona repository locations, and
enables the listed repository location after that. The following example first
disables all Percona repository locations and then enables `psmdb-40
experimental`:

```
$ sudo percona-release enable-only psmdb-40 experimental
```


* `disable` disables the specified repositories (or just `all` of them).
For example, following command will disable all repository locations:

```
$ sudo percona-release disable all
```

!!! note

    The `prel` repository remains enabled. This repository stores the `percona-release` packages and is always enabled for `percona-release` to operate.


* `setup` `<PRODUCT>` command disables all current Percona
repository locations, then enables the correct release repositories given a
*product use*, and updates the platform’s package manager database.
`<PRODUCT>` is the only parameter of this command, and it can be
chosen from the following table (the names of products are self-explanatory):

???+ admonition "**Product list**"

    |  Product        |  Product        | Product         | Product         |
    |                 |                 |                 |                 |
    |  ``ps56``       | ``ppg11``       | ``pdmdb4.2``    | ``pdps8.0``     |
    |  ``ps57``       | ``ppg11.5``     | ``pdmdb4.2.6``  | ``pdps8.0.19``  |
    |  ``ps80``       | ``ppg11.6``     | ``pdmdb4.2.7``  | ``pdps8.0.20``  |
    |  ``pxb24``      | ``ppg11.7``     | ``pdmdb4.2.8``  | ``pdps8.0.21``  |
    |  ``pxb80``      | ``ppg11.8``     | ``pdmdb4.2.9``  | ``pdps8.0.22``  |
    |  ``pxc56``      | ``ppg11.9``     | ``pdmdb4.2.10`` | ``pdps8.0.23``  |
    |  ``pxc57``      | ``ppg11.10``    | ``pdmdb4.2.11`` | ``pdps8.0.25``  |
    |  ``pxc80``      | ``ppg11.12``    | ``pdmdb4.2.12`` | ``pdpxc8.0``    |
    | ``pbm``         | ``ppg12``       | ``pdmdb4.2.13`` | ``pdpxc8.0.19`` |
    | ``psmdb34``     | ``ppg12.1``     | ``pdmdb4.2.14`` | ``pdpxc8.0.20`` |
    | ``psmdb36``     | ``ppg12.2``     | ``pdmdb4.2.15`` | ``pdpxc8.0.21`` |
    | ``psmdb40``     | ``ppg12.3``     | ``pdmdb4.4``    | ``pdpxc8.0.22`` |
    | ``psmdb42``     | ``ppg12.4``     | ``pdmdb4.4.0``  | ``pdpxc8.0.23`` |
    | ``psmdb44``     | ``ppg12.5``     | ``pdmdb4.4.1``  |  |
    |                 | ``ppg12.6``     | ``pdmdb4.4.2``  |  |
    |``mysql-shell``  | ``ppg12.7``     | ``pdmdb4.4.3``  |  |
    | ``sysbench``    | ``ppg13``       | ``pdmdb4.4.4``  |  |
    | ``proxysql``    | ``ppg13.1``     | ``pdmdb4.4.5``  |  |
    | ``pt``          | ``ppg13.2``     | ``pdmdb4.4.6``  |   |
    | ``pmm-client``  | ``ppg13.3``     |  |   |
    | ``pmm2-client`` |  |   |   |
    | ``prel``        |  |   |   | 

&nbsp;  

The following example disables all Percona repository locations and then
enables the `release` repository for *Percona Server for MySQL* 8.0. This
command runs in the interactive mode and may request extra input from you,
depending on your platform.

```
percona-release setup ps80
```

In non-interactive contexts, such as in scripts, requests for extra input may
halt the program.  Run the `setup` command with the -y option to provide
the affirmative answer where input from the user would be requested in the
interactive mode.

```
percona-release setup -y ps80
```

### Repository locations

*Repository location* may contain two parts: a *repository* and a *component*.
Available repositories are:

??? admonition "**MySQL Software**"

     
    | Repository    | Product Packages                |
    | ----------    | ------------------------------- |
    | `ps-56`       | Percona Server for MySQL 5.6    |
    | `ps-57`       | Percona Server for MySQL 5.7    |
    | `ps-80`       | Percona Server for MySQL 8.0    |
    | `pxc-56`      | Percona XtraDB Cluster 5.6      |
    | `pxc-57`      | Percona XtraDB Cluster 5.7      |
    | `pxc-80`      | Percona XtraDB Cluster 8.0      |
    | `pxb-24`      | Percona XtraBackup 2.4          |
    | `pxb-80`      | Percona XtraBackup 8.0          |
    | `pdps-8.0`    |Percona Distribution for MySQL using Percona Server for MySQL 8.0  |
    | `pdps-8.0.19` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.19|
    | `pdps-8.0.20` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.20 |
    | `pdps-8.0.21` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.21 |
    | `pdps-8.0.22` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.22 |
    | `pdps-8.0.23` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.23 |
    | `pdps-8.0.25` |Percona Distribution for MySQL using Percona Server for MySQL 8.0.25 |
    | `pdpxc-8.0`   |Percona Distribution for MySQL using Percona XtraDB Cluster 8.0  |
    | `pdpxc-8.0.19`|Percona Distribution for MySQL using Percona XtraDB Cluster 8.0.19|
    | `pdpxc-8.0.20`|Percona Distribution for MySQL using Percona XtraDB Cluster 8.0.20 |
    | `pdpxc-8.0.21`|Percona Distribution for MySQL using Percona XtraDB Cluster 8.0.21 |
    | `pdpxc-8.0.22`|Percona Distribution for MySQL using Percona XtraDB Cluster 8.0.22 |
    | `pdpxc-8.0.23`|Percona Distribution for MySQL using Percona XtraDB Cluster 8.0.23 |
  
&nbsp;  

??? admonition "**MongoDB Software**"

    | Repository    | Product Packages                        |
    | ------------- | ------------------------------------    |
    | `psmdb-36`    | Percona Server for MongoDB 3.6          |
    | `psmdb-40`    | Percona Server for MongoDB 4.0          |
    | `psmdb-42`    | Percona Server for MongoDB 4.2          |
    | `psmdb-44`    | Percona Server for MongoDB 4.4          |
    | `pbm`         | Percona Backup for MongoDB              |
    | `pdmdb-4.2`   | Percona Distribution for MongoDB 4.2    |
    | `pdmdb-4.2.6` | Percona Distribution for MongoDB 4.2.6  |
    | `pdmdb-4.2.7` | Percona Distribution for MongoDB 4.2.7  |
    | `pdmdb-4.2.8` | Percona Distribution for MongoDB 4.2.8  |
    | `pdmdb-4.2.9` | Percona Distribution for MongoDB 4.2.9  |
    | `pdmdb-4.2.10`| Percona Distribution for MongoDB 4.2.10 |
    | `pdmdb-4.2.11`| Percona Distribution for MongoDB 4.2.11 |
    | `pdmdb-4.2.12`| Percona Distribution for MongoDB 4.2.12 |
    | `pdmdb-4.2.13`| Percona Distribution for MongoDB 4.2.13 |
    | `pdmdb-4.2.14`| Percona Distribution for MongoDB 4.2.14 |
    | `pdmdb-4.2.15`| Percona Distribution for MongoDB 4.2.15 |
    | `pdmdb-4.4`   | Percona Distribution for MongoDB 4.4    |
    | `pdmdb-4.4.0` | Percona Distribution for MongoDB 4.4.0  |
    | `pdmdb-4.4.1` | Percona Distribution for MongoDB 4.4.1  |
    | `pdmdb-4.4.2` | Percona Distribution for MongoDB 4.4.2  |
    | `pdmdb-4.4.3` | Percona Distribution for MongoDB 4.4.3  |
    | `pdmdb-4.4.4` | Percona Distribution for MongoDB 4.4.4  |
    | `pdmdb-4.4.5` | Percona Distribution for MongoDB 4.4.5  |
    | `pdmdb-4.4.6` | Percona Distribution for MongoDB 4.4.6  |

&nbsp;  

??? admonition "**PostgreSQL Software**"

    | Repository    | Product Packages                          |
    | ------------- | ----------------------------------------- |
    | `ppg-11`      | Percona Distribution for PostgreSQL 11    |
    | `ppg-11.5`    | Percona Distribution for PostgreSQL 11.5  |
    | `ppg-11.6`    | Percona Distribution for PostgreSQL 11.6  |
    | `ppg-11.7`    | Percona Distribution for PostgreSQL 11.7  |
    | `ppg-11.8`    | Percona Distribution for PostgreSQL 11.8  |
    | `ppg-11.9`    | Percona Distribution for PostgreSQL 11.9  |
    | `ppg-11.10`   | Percona Distribution for PostgreSQL 11.10 |
    | `ppg-11.11`   | Percona Distribution for PostgreSQL 11.11 |
    | `ppg-11.12`   | Percona Distribution for PostgreSQL 11.12 |
    | `ppg-12`      | Percona Distribution for PostgreSQL 12    |
    | `ppg-12.2`    | Percona Distribution for PostgreSQL 12.2  |
    | `ppg-12.3`    | Percona Distribution for PostgreSQL 12.3  |
    | `ppg-12.4`    | Percona Distribution for PostgreSQL 12.4  |
    | `ppg-12.5`    | Percona Distribution for PostgreSQL 12.5  |
    | `ppg-12.6`    | Percona Distribution for PostgreSQL 12.6  |
    | `ppg-12.7`    | Percona Distribution for PostgreSQL 12.7  |
    | `ppg-13`      | Percona Distribution for PostgreSQL 13    |
    | `ppg-13.0`    | Percona Distribution for PostgreSQL 13.0  |
    | `ppg-13.1`    | Percona Distribution for PostgreSQL 13.1  |
    | `ppg-13.2`    | Percona Distribution for PostgreSQL 13.2  |
    | `ppg-13.3`    | Percona Distribution for PostgreSQL 13.3  |

&nbsp;  

??? admonition "**Percona Tools**"

    | Repository    | Product Packages                          |
    | ------------- | ----------------------------------------- |
    | `pmm-client`  | Percona Monitoring and Management Client  |
    | `pmm2-client` | Percona Monitoring and Management Client 2|
    | `pt`          | Percona Toolkit                           |
    | `proxysql`    | ProxySQL                                  |
    | `mysql-shell` | MySQL Shell                               |
    | `sysbench`    | Sysbench tool for benchmarking            |
    | `original`    | Percona’s products of previous versions which haven’t yet reached their end of life and are still supported. These are: Percona Server for MySQL 5.6 and 5.7, Percona XtraDB Cluster 5.6 and 5.7, Percona Server for MongoDB 3.4 and 3.6, etc. Though moved to dedicated repositories, they are kept here for backward compatibility |
    | `tools`       | Other products and tools, such as Percona XtraBackup 8.0, Percona Toolkit, PMM Client, ProxySQL, etc. Though moved to dedicated repositories, they are kept here for backward compatibility |
    | `prel`        | percona-release packages                  |

&nbsp;    

### Components

By using a component you may choose to use either the GA version of the selected
product or its beta version. **percona-release** recognizes `release` (used by
default), `testing`, and `experimental` components.

| Component     | Usage                                     |
| ------------- | ----------------------------------------- |
| `release`     | Stores released GA packages of products.  |
| `testing`     | Is used for final QA and package testing for GA candidate packages of products. |
| `experimental`| Hosts alpha and beta releases of products |

For example, to prepare your system for installation of *Percona Server for MySQL*
8.0, run `percona-release` as follows:

```
sudo percona-release enable-only ps-80 release
```

To enable pre-release builds from the testing repository, run **percona-release**
with the `testing` component.

```
sudo percona-release enable ps-80 testing
```

This example enables installing a pre-release version of Percona Server for MySQL 8.0.

## Examples: All steps for installing a specific Percona product

### Percona XtraDB Cluster 8.0 on CentOS 7:

```
sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
sudo percona-release enable-only pxc-80 release
sudo percona-release enable tools release
sudo yum install percona-xtradb-cluster
```

### Percona Server for MySQL 8.0, Percona Toolkit, Percona XtraBackup and Sysbench on Ubuntu 18.04:

```
wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
sudo dpkg -i percona-release_latest.generic_all.deb
sudo percona-release enable-only ps-80 release
sudo percona-release enable tools release
sudo apt-get update
sudo apt-get install percona-server-server percona-server-client percona-toolkit percona-xtrabackup-80 sysbench
```

### Percona Server for MySQL 8.0 release package on CentOS or other RPM-based systems:

```
sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
sudo percona-release setup ps80
sudo yum install percona-server-server
```

### Percona Server for MongoDB 4.2 release package on Ubuntu or another DEB-based GNU/Linux distribution:

```
wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
sudo dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb
sudo percona-release setup psmdb42
sudo apt-get install percona-server-mongodb-42
```

## Updating **percona-release** to the latest version

**percona-release** itself is available from the *prel* repository which is enabled by default. Thus, to update **percona-release**, simply run the following command as root or via sudo:


* For Debian and Ubuntu:

  
   1. Update the local cache

      ```
      apt-get update
      ```

   2. Update percona-release
  
      ```   
      apt-get install percona-release
      ```

* For RHEL/CentOS:

   ```
   yum update percona-release
   ```