# Configuring Percona Repositories with `percona-release`

The `percona-release` configuration tool allows users to automatically configure
which [Percona Software repositories](repository-location.md) are enabled or
disabled. It supports both `apt` and `yum` repositories.

## Usage

`percona-release` has the following syntax:

```sh
percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all]
```

Run all commands as the root user or via `sudo`. 

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

`<PRODUCT>` is the only parameter of this command, please refer to
[Repostory locations](repository-location.md) for an overview of the available
product repositories.

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
curl -O https://repo.percona.com/apt/percona-release_latest.generic_all.deb
sudo apt install ./percona-release_latest.generic_all.deb
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
curl -O https://repo.percona.com/apt/percona-release_latest.generic_all.deb
sudo apt install ./percona-release_latest.generic_all.deb
sudo percona-release setup psmdb42
sudo apt install percona-server-mongodb-42
```
