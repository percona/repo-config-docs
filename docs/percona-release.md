# Configure Percona repositories with `percona-release`

The `percona-release` configuration tool enables users to automatically
configure which [Percona Software repositories](repository-location.md) are
enabled or disabled. It supports both `apt` and `yum` repositories.

## Usage

`percona-release` has the following syntax:

```{.bash data-prompt="$"}
percona-release <COMMAND> (<REPOSITORY> | all) [<COMPONENT> | all] [<FLAGS>]
```

Run all commands as the root user or via `sudo`. 

### Commands

Available commands are [enable](#enable), [enable-only](#enable-only), [disable](#disable), [setup](#setup) and [show](#show):


#### `show` 

The command shows the enabled repositories in your system:

```{.bash data-prompt="$"}
$ sudo percona-release show
```


#### `enable`

The command turns on an additional Percona [repository location](repository-location.md).
For example, the following command enables the `ps-80 release` repository
location:

```{.bash data-prompt="$"}
$ sudo percona-release enable ps-84-lts release
```


#### `enable-only` 

This command turns off all Percona repository locations, and
enables the listed repository location after that. The following example first
disables all Percona repository locations and then enables `psmdb-40
experimental`:

```{.bash data-prompt="$"}
$ sudo percona-release enable-only psmdb-40 experimental
```


#### `disable`

The command disables the specified repositories. The `all` flag disables all repositories.

For example, the following command will disable all repository locations:

```{.bash data-prompt="$"}
$ sudo percona-release disable all
```

!!! note

    The `prel` repository remains enabled. This repository stores the `percona-release` packages and is always enabled for `percona-release` to operate.


#### `setup`

The `setup` `<PRODUCT>` command disables all current Percona
repository locations, then enables the correct release repositories given a
*product use*, and updates the platform’s package manager database.

`<PRODUCT>` is the only parameter of this command, please refer to
[Repository locations](repository-location.md) for an overview of the available
product repositories.

The following example disables all Percona repository locations and then
enables the `release` repository for *Percona Server for MySQL* 8.0. This
command runs in the interactive mode and may request extra input from you,
depending on your platform.

```{.bash data-prompt="$"}
$ percona-release setup ps-84-lts
```

In non-interactive contexts, such as in scripts, requests for extra input may
halt the program. Run the `setup` command with the `-y` option to provide
the affirmative answer where input from the user would be requested in the
interactive mode.

```{.bash data-prompt="$"}
$ percona-release setup -y ps-84-lts
```

### Flags

Available flags are: [`--scheme`](#scheme)

#### `--scheme`

The `--scheme` flag enables you to choose what protocol to use when enabling repositories. Available options are HTTP and HTTPS. Default value is HTTP.

This flag is useful when you want to use HTTPS for security reasons or when your environment requires it.

For example, to use `https` when accessing the repository URL, run the following command:

```{.bash data-prompt="$"}
$ sudo percona-release enable ps-84-lts release --scheme https
```

If no `--scheme` flag is specified, the default HTTP protocol is used. 

You can use this flag with the `enable`, `enable-only`, `disable`, and `setup` commands.


## Examples: All steps for installing a specific Percona product

### Percona XtraDB Cluster 8.4 on RHEL 9:

```{.bash data-prompt="$"}
$ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
$ sudo percona-release enable-only pxc-84-lts release
$ sudo yum install percona-xtrabackup-84
```

### Percona Server for MySQL 8.0, Percona Toolkit, and Sysbench on Ubuntu 24.04:

```{.bash data-prompt="$"}
$ sudo apt update
$ sudo apt install curl
$ curl -O https://repo.percona.com/apt/percona-release_latest.generic_all.deb
$ sudo apt install gnupg2 lsb-release ./percona-release_latest.generic_all.deb
$ sudo apt update
$ sudo percona-release enable-only ps-84-lts release
$ sudo percona-release enable pt release
$ sudo apt install percona-server-server percona-toolkit  sysbench
```

### Percona Server for MySQL 8.4 release package on RPM-based systems:

```{.bash data-prompt="$"}
$ sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm
$ sudo percona-release setup ps-84-lts
$ sudo percona-release enable ps-84-lts release
$ sudo yum install percona-server-server
```

### Percona Server for MongoDB 8.0 release package on Ubuntu or another DEB-based GNU/Linux distribution:

```{.bash data-prompt="$"}
$ wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb
$ sudo dpkg -i percona-release_latest.$(lsb_release -sc)_all.deb
$ sudo percona-release setup psmdb-80 release
$ sudo apt install percona-server-mongodb
```
