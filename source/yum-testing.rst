.. _yum-testing:

============================================================================
Testing and Experimental Repositories on Red Hat Enterprise Linux and CentOS
============================================================================

Percona offers pre-release builds from the testing repo,
and early-stage development builds from the experimental repo.
You can enable either one in the Percona repository configuration file
:file:`/etc/yum.repos.d/percona-release.repo`.
There are three sections in this file,
for configuring corresponding repositories:

* stable release
* testing
* experimental

The latter two repositories are disabled by default.

If you want to install the latest testing builds,
set ``enabled=1`` for the following entries: ::

  [percona-testing-$basearch]
  [percona-testing-noarch]

If you want to install the latest experimental builds,
set ``enabled=1`` for the following entries: ::

  [percona-experimental-$basearch]
  [percona-experimental-noarch]
