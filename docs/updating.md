# Updating `percona-release` to the latest version

`percona-release` itself is available from the *prel* repository which is enabled by default. Thus, to update `percona-release`, simply run the following command as root or via `sudo`:

=== "Debian and Ubuntu Linux"
  
   1. Update the local cache first

      ``` sh
      sudo apt update
      ```

   2. Update `percona-release`
  
      ``` sh
      sudo apt upgrade percona-release
      ```

=== "Red Hat Enterprise Linux (and compatible derivatives)"

   ``` sh
   sudo yum update percona-release
   ```
