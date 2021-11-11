# Configuring Percona Repositories with percona-release

The **percona-release** configuration tool allows users to automatically
configure which Percona repositories are enabled and disabled.

## Usage

`percona-release` has the following syntax:

```sh
percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]
```
Run all commands as root or via `sudo`. 

### Commands

Available commands are [enable](#enable), [enable-only](#enable-only), [disable](#disable), [setup](#setup) and [show](#show):


#### `show` 

The command shows the enabled repositories in your system:

``` sh
sudo percona-release show
```


#### `enable`

The command turns on an additional Percona [repository location](repository-location.md).
For example, the following command enables the `ps-80 release` repository
location:

```sh
sudo percona-release enable ps-80 release
```


#### `enable-only` 

This command turns off all Percona repository locations, and
enables the listed repository location after that. The following example first
disables all Percona repository locations and then enables `psmdb-40
experimental`:

```sh
sudo percona-release enable-only psmdb-40 experimental
```


#### `disable`

The command disables the specified repositories. The `all` flag disables all repositories.

For example, the following command will disable all repository locations:

```
$ sudo percona-release disable all
```

!!! note

    The `prel` repository remains enabled. This repository stores the `percona-release` packages and is always enabled for `percona-release` to operate.


#### `setup`

The `setup` `<PRODUCT>` command disables all current Percona
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
    |  ``pxc80``      | ``ppg11.12``    | ``pdmdb4.2.12`` | ``pdps8.0.26``  |
    | ``pbm``         | ``ppg11.13``    | ``pdmdb4.2.13`` | ``pdpxc8.0``    |
    | ``psmdb34``     | ``ppg12``       | ``pdmdb4.2.14`` | ``pdpxc8.0.19`` |
    | ``psmdb36``     | ``ppg12.1``     | ``pdmdb4.2.15`` | ``pdpxc8.0.20`` |
    | ``psmdb40``     | ``ppg12.2``     | ``pdmdb4.2.17`` | ``pdpxc8.0.21`` |
    | ``psmdb42``     | ``ppg12.3``     | ``pdmdb4.4``    | ``pdpxc8.0.22`` |
    | ``psmdb44``     | ``ppg12.4``     | ``pdmdb4.4.0``  | ``pdpxc8.0.23`` |
    | ``psmdb50``     | ``ppg12.5``     | ``pdmdb4.4.1``  |  |
    |``mysql-shell``  | ``ppg12.6``     | ``pdmdb4.4.2``  |  |
    | ``sysbench``    | ``ppg12.7``     | ``pdmdb4.4.3``  |  |
    | ``proxysql``    | ``ppg12.8``     | ``pdmdb4.4.4``  |  |
    | ``pt``          | ``ppg13``       | ``pdmdb4.4.5``  |   |
    | ``pmm-client``  | ``ppg13.1``     | ``pdmdb4.4.6``  |   |
    | ``pmm2-client`` | ``ppg13.2``     | ``pdmdb4.4.8``  |   |
    | ``prel``        | ``ppg13.3``     | ``pdmdb4.4.9``  |   |
    |                 | ``ppg13.4``     | ``pdmdb4.4.10`` |   |


&nbsp;  

The following example disables all Percona repository locations and then
enables the `release` repository for *Percona Server for MySQL* 8.0. This
command runs in the interactive mode and may request extra input from you,
depending on your platform.

```
percona-release setup ps80
```

In non-interactive contexts, such as in scripts, requests for extra input may
halt the program.  Run the `setup` command with the `-y` option to provide
the affirmative answer where input from the user would be requested in the
interactive mode.

```
percona-release setup -y ps80
```
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
sudo apt update
sudo apt install percona-server-server percona-server-client percona-toolkit percona-xtrabackup-80 sysbench
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
sudo apt install percona-server-mongodb-42
```

