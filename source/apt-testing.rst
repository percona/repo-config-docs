.. _apt-testing:

==========================================================
Testing and Experimental Repositories on Debian and Ubuntu
==========================================================

Percona offers pre-release builds from the testing repo,
and early-stage development builds from the experimental repo.
To enable them, add either ``testing`` or ``experimental`` at the end
of the Percona repository definition in your repository file
(by default, :file:`/etc/apt/sources.list.d/percona-release.list`).

For example, if you are running Debian 8 ("jessie")
and want to install the latest testing builds,
the definitions should look like this::

  deb http://repo.percona.com/apt jessie main testing
  deb-src http://repo.percona.com/apt jessie main testing

If you are running Ubuntu 14.04 LTS (Trusty Tahr)
and want to install the latest experimental builds,
the definitions should look like this::

  deb http://repo.percona.com/apt trusty main experimental
  deb-src http://repo.percona.com/apt trusty main experimental

