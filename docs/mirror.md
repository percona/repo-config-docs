# Create a local mirror of a Percona repository

Enterprises introduce various security policies: for example, allow Internet access only on one server or deny root privileges to database administrators. 

To comply with these policies and install Percona software in your environment, a solution is to set up the local mirror of Percona repositories. This document provides instructions how to do it.

!!! important

    The instructions below are for AMD/Intel x64 architectures. 

## Prerequisites

To create a local mirror of a Percona repository, you need the following software:

* Rsync to download packages from Percona repositories and upload them to your mirror
* Repository creation tools:

    - `dpkg-dev` for Debian and Ubuntu
    - `createrepo` for RHEL and derivatives

## Debian and Ubuntu

1. Install `dpkg-dev` utility to unpack, build and upload Debian source packages.

    ```{.bash data-prompt="$"}
    $ sudo apt install dpkg-dev
    ```

2. Create the folder where your mirror repository resides. For example, `/opt/debs/`

    ```{.bash data-prompt="$"}
    $ sudo mkdir -p /opt/debs/
    ```

3. Download the `.deb` packages relevant to your operating system from Percona repository into your repository using `rsync`:

    ```{.bash data-prompt="$"}
    $ rsync -avrt rsync://rsync.percona.com/rsync/<repo-name>/apt/pool/main/p/<product_name>/*.<os-version>*.deb /opt/debs/
    ```

    For example, to download Percona Backup for MongoDB packages on Ubuntu 22.04, the command is the following:

    ```{.bash .no-copy}
    $ rsync -avrt rsync://rsync.percona.com/rsync/pbm/apt/pool/main/p/percona-backup-mongodb/*.jammy*.deb /opt/debs/
    ```
    
    Check the list of available repositories for [MySQL](mysql.md), [MongoDB](mongodb.md), [PostgreSQL](postgresql.md) and [Percona Tools](tools.md).

4. Create the Packages file. This is the file that the package manager uses to retrieve the information about new and updated packages when you run `apt-get update`. Use the `dpkg-scanpackages` command:

    ```{.bash data-prompt="$"}
    $ cd /opt/debs
    $ dpkg-scanpackages . /dev/null > Packages
    ```

    The command adds the latest version of the packages to the Packages file.

5. Import the GPG key to sign the repository.

    ```{.bash data-prompt="$"}
    $ curl -fsSL https://github.com/percona/percona-repositories/raw/main/deb/percona-keyring.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/percona-keyring.gpg >/dev/null
    ```

6. Add your repository to the `etc/apt/sources.list` file for the package manager to find new or updated packages from your repository:
   
    ```{.bash data-prompt="$"}
    $ echo "deb [trusted=yes] file:///opt/debs ./" | sudo tee -a /etc/apt/sources.list
    ```

7. Run `apt-get update` to check that the package manager can read from your repository.

8. (Optional) Check your mirror repository contents:

    ```{.bash data-prompt="$"}
    $ apt-cache policy percona-backup-mongodb 
    ```

    ??? example "Sample output"

        ``` {.text .no-copy}
        percona-backup-mongodb: 
         Installed: (none) 
         Candidate: 2.3.1-1.jammy 
         Version table: 
            2.3.1-1.jammy 500 
               500 file:/opt/debs ./ Packages
        ```


## RHEL and derivatives

1. Install the `createrepo` utility. It creates yum repositories and their metadata caches

    ```{.bash data-prompt="$"}
    $ sudo yum install createrepo
    ```

2. Create the directory where your mirror repository resides. For example, `/opt/rpms`

    ```{.bash data-prompt="$"}
    $ sudo mkdir /opt/rpms
    ```

3. Create the repository metadata using `createrepo`

    ```{.bash data-prompt="$"}
    $ sudo createrepo /opt/rpms
    ```

4. Download RPM packages from Percona repository to your local mirror using `rsync`:

    ```{.bash data-prompt="$"}
    $ rsync -avrt rsync://rsync.percona.com/rsync/<repo_name>/yum/release/<os_version>/RPMS/x86_64/ /opt/rpms/
    ```

    For example, to download packages for Percona Distribution for PostgreSQL 15 on Oracle Linux 9, the command is the following:

    ```{.bash .no-copy}
    rsync -avrt rsync://rsync.percona.com/rsync/ppg-15/yum/release/9/RPMS/x86_64/ /opt/rpms/
    ```
    
     Check the list of available repositories for [MySQL](mysql.md), [MongoDB](mongodb.md), [PostgreSQL](postgresql.md) and [Percona Tools](tools.md).

5. Update the repository metadata:

    ```{.bash data-prompt="$"}
    $ sudo createrepo --update /opt/rpms
    ```

6. Import the GPG key to sign the repository:

    ```{.bash data-prompt="$"}
    $ curl -s https://raw.githubusercontent.com/percona/percona-repositories/release-1.0-27/rpm/RPM-GPG-KEY-Percona | sudo rpm --import -
    ```

7. Create the repository configuration file. It must meet the following criteria:

    * It must be located in `/etc/yum.repos.d/` 
    * It must have the extension `.repo` to be recognized by `yum`.

    The following is the example of the configuration file:

    ```init title="/etc/yum.repos.d/percona-local.repo"
    [percona-local]
    name=Local Percona repository
    baseurl=file:///opt/rpms/
    gpgcheck=1
    enabled=1
    ```

8. Check the setup:

    ```{.bash data-prompt="$"}
    $ rpm -q gpg-pubkey --qf '%{NAME}-%{VERSION}-%{RELEASE}\t%{SUMMARY}\n'
    ```

## Keep the mirror repository up-to-date

To update your local mirror, do the following:

=== "Debian and Ubuntu"

    1. Download new packages relevant to your operating system from Percona repository

        ```{.bash data-prompt="$"}
        $ rsync -avrt rsync://rsync.percona.com/rsync/<repo-name>/apt/pool/main/p/<product_name>/*.<os-version>*.deb /opt/debs/
        ```

    2. Update the Packages file.

        ```{.bash data-prompt="$"}
        $ cd /opt/debs
        dpkg-scanpackages . /dev/null > Packages
        ```

    3. Update the local cache.

        ```{.bash data-prompt="$"}
        $ apt update
        ```

=== "RHEL and derivatives"

    1. Download new packages from Percona repository

        ```{.bash data-prompt="$"}
        $ rsync -avrt rsync://rsync.percona.com/rsync/<repo_name>/yum/release/<os_version>/RPMS/x86_64/ /opt/rpms/
        ```

    2. Update the repository metadata

        ```{.bash data-prompt="$"}
        $ sudo createrepo --update /opt/rpms
        ```

!!! tip

    You can automate the download process by adding the task to `crontab`.

!!! admonition ""

    Based on the blog post [How to Create Your Own Repositories for Packages](https://www.percona.com/blog/how-to-create-your-own-repositories-for-packages/) by *Evgeniy Patlan*
