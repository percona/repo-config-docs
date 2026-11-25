# MySQL software repositories

| Repository         | Product Packages                    |
| ------------------ | ----------------------------------- |
| `ps-97-lts`        | Percona Server for MySQL 9.7        |
| `ps-84-lts`        | Percona Server for MySQL 8.4        |
| `ps-8x-innovation` | Percona Server for MySQL 8.3        |
| `ps-80`            | Percona Server for MySQL 8.0        |
| `ps-57`            | Percona Server for MySQL 5.7        |
| `pxc-97-lts`       | Percona XtraDB Cluster 9.7          |
| `pxc-84-lts`       | Percona XtraDB Cluster 8.4          |
| `pxc-80`           | Percona XtraDB Cluster 8.0          |
| `pxc-57`           | Percona XtraDB Cluster 5.7          |
| `pxc-56`           | Percona XtraDB Cluster 5.6          |
| `pxb-97-lts`       | Percona XtraBackup 9.7              |
| `pxb-84-lts`       | Percona XtraBackup 8.4              |
| `pxb-8x-innovation`| Percona XtraBackup 8.3              |
| `pxb-80`           | Percona XtraBackup 8.0              |
| `pxb-24`           | Percona XtraBackup 2.4              |

## Percona Distribution for MySQL

Percona Distribution for MySQL is available in two variants:

* Percona Distribution for MySQL (PDPS): based on Percona Server for MySQL
* Percona Distribution for MySQL (PDPXC): based on Percona XtraDB Cluster

Each LTS release (8.4, 9.7) has a corresponding Distribution release in each variant.

| Repository     | Description                                                                |
| -------------- | -------------------------------------------------------------------------- |
| `pdps-97-lts`  | Percona Distribution for MySQL based on Percona Server for MySQL 9.7 (LTS) |
| `pdpxc-97-lts` | Percona Distribution for MySQL based on Percona XtraDB Cluster 9.7 (LTS)   |
| `pdps-84-lts`  | Percona Distribution for MySQL based on Percona Server for MySQL 8.4 (LTS) |
| `pdpxc-84-lts` | Percona Distribution for MySQL based on Percona XtraDB Cluster 8.4 (LTS)   |
| `pdps-8.0`     | Percona Distribution for MySQL based on Percona Server for MySQL 8.0       |
| `pdpxc-8.0`    | Percona Distribution for MySQL based on Percona XtraDB Cluster 8.0         |

### Pin to a minor release

To stay on a specific minor release, use `pdps-<version>` or `pdpxc-<version>`. For example, `pdps-8.4.8` or `pdpxc-9.7.2`. Not every minor release has a pinned repository.

### Innovation releases

Innovation-track repositories are available for Percona Distribution for MySQL based on Percona Server for MySQL only: `pdps-8x-innovation` and `pdps-8.1.0` through `pdps-8.3.0`.
