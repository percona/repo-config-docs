# Repository locations

*Repository location* may contain two parts: a repository and a component.

## Components

By using a component you may choose to use either the GA version of the selected
product or its beta version. **percona-release** recognizes `release` (used by
default), `testing`, and `experimental` components.

| Component     | Usage                                     |
| ------------- | ----------------------------------------- |
| `release`     | Stores released GA packages of products.  |
| `testing`     | Is used for final QA and package testing for GA candidate packages of products. |
| `experimental`| Hosts alpha and beta releases of products |

For example, to prepare your system for installation of *Percona Server for MySQL*
8.4, run `percona-release` as follows:

```{.bash data-prompt="$"}
$ sudo percona-release enable-only ps-84-lts release
```

To enable pre-release builds from the testing repository, run **percona-release**
with the `testing` component.

```{.bash data-prompt="$"}
$ sudo percona-release enable ps-84-lts testing
```

This example enables installing a pre-release version of Percona Server for MySQL 8.4.

