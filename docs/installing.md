# Install percona-release

It is recommended to install Percona software using the corresponding package manager
for your system:

* **apt** for Debian and Ubuntu Linux
* **yum** for Red Hat Enterprise Linux and compatible derivatives (including CentOS, Oracle Linux, Amazon Linux AMI, etc.)

You can find information about the supported platforms on the [Percona Release Lifecycle Overview :octicons-link-external-16:](https://www.percona.com/services/policies/percona-software-support-lifecycle#support) page.

## 1. Choose your package manager

=== ":material-debian: On Debian and Ubuntu"

    If you are running a DEB-based distribution, such as Debian or Ubuntu Linux, use
    the **apt** package manager to install the `percona-release` official package:

    1. Install the `curl` download utility if it's not installed already:

        ```{.bash data-prompt="$"}
        $ sudo apt update
        $ sudo apt install curl 
        ```

    2. Download the `percona-release` repository package:

        ```{.bash data-prompt="$"}
        $ curl -O https://repo.percona.com/apt/percona-release_latest.generic_all.deb
        ```

    3. Install the downloaded repository package and its dependencies using `apt`:

        ```{.bash data-prompt="$"}
        $ sudo apt install gnupg2 lsb-release ./percona-release_latest.generic_all.deb
        ```

    4. Refresh the local cache to update the package information:

        ```{.bash data-prompt="$"}
        $ sudo apt update
        ```

    5. After installation, the *Percona* software repositories are available. You
    can check the repository setup for the Percona original release list in the
    `/etc/apt/sources.list.d/percona-original-release.list` file.

        !!! note
            If you have enabled another repository, the file name will be different.

=== ":material-redhat: On Red Hat Enterprise Linux and compatible derivatives"

    If you are running an RPM-based Linux distribution, such as Red Hat Enterprise
    Linux or compatible derivatives, use the `yum` package manager to install
    `percona-release`.

    Run the following command as the `root` user or with `sudo`:

    ```{.bash data-prompt="$"}
    $ sudo yum install -y https://repo.percona.com/yum/percona-release-latest.noarch.rpm
    ```

## 2. Set up the repository

Use the `percona-release` command to [setup the repository](repository-location.md) that contains the Percona product that you intend to install:

```{.bash data-prompt="$"}
$ sudo percona-release setup <PRODUCT>
```

!!! note
    See [Configuring Percona Repositories with `percona-release`](percona-release.md) for additional information.

## 3. Install the product package

Use the operating system's package management tool to install the desired product package.

=== ":material-debian: Debian and Ubuntu"

    * [Percona Distribution for MongoDB :octicons-link-external-16:](https://docs.percona.com/percona-distribution-for-mongodb/latest/installation.html#install-on-debian-ubuntu) (EOL)
    * [Percona Distribution for MySQL :octicons-link-external-16:](https://docs.percona.com/percona-distribution-for-mysql/{{ppmysqllatest}}/installing.html)
    * [Percona Distribution for PostgreSQL :octicons-link-external-16:](https://docs.percona.com/postgresql/{{ppglatest}}/apt.html)
    * [Percona Server for MySQL :octicons-link-external-16:](https://docs.percona.com/percona-server/{{ppsmysqllatest}}/apt-repo.html)
    * [Percona Server for MongoDB :octicons-link-external-16:](https://docs.percona.com/percona-server-for-mongodb/{{ppserverlatest}}/install/apt.html)
    * [Percona XtraBackup :octicons-link-external-16:](https://docs.percona.com/percona-xtrabackup/{{pxtralatest}}/apt-repo.html)
    * [Percona XtraDB Cluster :octicons-link-external-16:](https://docs.percona.com/percona-xtradb-cluster/{{pxtraclusterlatest}}/apt.html)

=== ":material-redhat: Red Hat Enterprise Linux and derivatives"

    * [Percona Distribution for MongoDB :octicons-link-external-16:](https://docs.percona.com/percona-distribution-for-mongodb/latest/installation.html#install-on-red-hat-enterprise-linux-centos) (EOL)
    * [Percona Distribution for MySQL :octicons-link-external-16:](https://docs.percona.com/percona-distribution-for-mysql/{{ppmysqllatest}}/installing.html)
    * [Percona Distribution for PostgreSQL :octicons-link-external-16:](https://docs.percona.com/postgresql/{{ppglatest}}/yum.html)
    * [Percona Server for MySQL :octicons-link-external-16:](https://docs.percona.com/percona-server/{{ppsmysqllatest}}/yum-repo.html)
    * [Percona Server for MongoDB :octicons-link-external-16:](https://docs.percona.com/percona-server-for-mongodb/{{ppserverlatest}}/install/yum.html)
    * [Percona XtraBackup :octicons-link-external-16:](https://docs.percona.com/percona-xtrabackup/{{pxtralatest}}/yum-repo.html)
    * [Percona XtraDB Cluster :octicons-link-external-16:](https://docs.percona.com/percona-xtradb-cluster/{{pxtraclusterlatest}}/yum.html)
