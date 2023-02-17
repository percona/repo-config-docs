# Update percona-release to the latest version

`percona-release` itself is available from the *prel* repository which is enabled by default. Thus, to update `percona-release`, simply run the following command as root or via `sudo`:

=== "Debian and Ubuntu Linux"
  
     1. Update the local cache first

        ```{.bash data-prompt="$"}
        $ sudo apt update
        ```

     2. Update `percona-release`
     
        ```{.bash data-prompt="$"}
        $ sudo apt upgrade percona-release
        ```

=== "Red Hat Enterprise Linux (and compatible derivatives)"

     ```{.bash data-prompt="$"}
     $ sudo yum update percona-release
     ```
