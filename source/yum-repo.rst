.. _yum-repo:

=====================================================================
Configuring Percona Repository on Red Hat Enterprise Linux and CentOS
=====================================================================

If you are running an RPM-based Linux distribution,
use the :command:`yum` package manager to install Percona software
from the official repository.

1. Install the repository package::

    sudo yum install http://www.percona.com/downloads/percona-release/redhat/0.1-6/percona-release-0.1-6.noarch.rpm

   You should see the following if successful::

    Installed:
      percona-release.noarch 0:0.1-6

    Complete!

#. Make sure that Percona packages are available::

    sudo yum list | grep percona

   You should see output similar to the following::

    percona-release.noarch                     0.1-6                       @/percona-release-0.1-6.noarch
    Percona-Server-55-debuginfo.x86_64         5.5.54-rel38.7.el7          percona-release-x86_64
    Percona-Server-56-debuginfo.x86_64         5.6.35-rel81.0.el7          percona-release-x86_64
    Percona-Server-57-debuginfo.x86_64         5.7.17-13.1.el7             percona-release-x86_64
    ...

