# Updating percona-release to the latest version

**percona-release** itself is available from the *prel* repository which is enabled by default. Thus, to update **percona-release**, simply run the following command as root or via sudo:


* For Debian and Ubuntu:

  
   1. Update the local cache

      ```
      apt update
      ```

   2. Update percona-release
  
      ```   
      apt install percona-release
      ```

* For RHEL/CentOS:

   ```
   yum update percona-release
   ```