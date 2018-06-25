# Ansible role `mariadb`

An ansible role for managing MariaDB.

* Install MariaDB packages from the official MariaDB repository.
* Set/Reset root password.
* Remove `test` database.
* Create users and databases
* Manage configuration file `my.cnf`

Fixed settings:
* Storage engine : InnoDB

Tested under:
* CentOS 7.4
* Fedora 25
* Ubuntu 16.04

## Requirements

No requirements

## Role Variables

| Variable                                 | Default           | Comments                                                                                                    |
|:-----------------------------------------|:------------------|:------------------------------------------------------------------------------------------------------------|
| `mariadb_bind_address`                   | '127.0.0.1'       | IP address of the network interface to listen on. '0.0.0.0' for all interfaces. |
| `mariadb_charset`                        | 'utf8'            | |
| `mariadb_collation`                      | 'utf8_general_ci' | |
| `mariadb_databases`                      | []                | databases to add. See [mysql_db](http://docs.ansible.com/ansible/devel/modules/mysql_db_module.html#parameters) |
| `mariadb_innodb_buffer_pool_instances`   | 8                 | |
| `mariadb_innodb_buffer_pool_size`        | 384M              | |
| `mariadb_innodb_file_format`             | Barracuda         | |
| `mariadb_innodb_file_format_check`       | 1                 | |
| `mariadb_innodb_file_per_table`          | ON                | |
| `mariadb_innodb_flush_log_at_trx_commit` | 1                 | |
| `mariadb_innodb_log_buffer_size`         | 16M               | |
| `mariadb_innodb_log_file_size`           | 48M               | |
| `mariadb_innodb_strict_mode`             | ON                | |
| `mariadb_join_buffer_size`               | 128K              | |
| `mariadb_log_warnings`                   | 1                 | 0: no warning logs. 1: critical warnings logged. >= 2: see manual. |
| `mariadb_long_query_time`                | 10                | |
| `mariadb_lower_case_table_names`         | 1                 | 0: case-sensitive(Linux), 1: stored in lowercase, case-insensitive(Windows), 2: stored as declared, compared in lowercase(OSX) |
| `mariadb_max_allowed_packet`             | 16M               | |
| `mariadb_max_connections`                | 151               | |
| `mariadb_max_heap_table_size`            | 16M               | |
| `mariadb_max_user_connections`           | 0                 | |
| `mariadb_port`                           | 3306              | port number |
| `mariadb_query_cache_size`               | 0                 | |
| `mariadb_read_buffer_size`               | 128K              | |
| `mariadb_read_rnd_buffer_size`           | 256k              | |
| `mariadb_root_password`                  | 'root'            | root password |
| `mariadb_root_remote`                    | `no`              | `yes`: enable remote root login |
| `mariadb_root_remote_host`               | '%'               | remote root login enabled host |
| `mariadb_skip_name_resolve`              | 1                 | |
| `mariadb_slow_query_log`                 | 0                 | |
| `mariadb_sort_buffer_size`               | 2M                | |
| `mariadb_table_definition_cache`         | 1400              | |
| `mariadb_table_open_cache`               | 2000              | |
| `mariadb_table_open_cache_instances`     | 8                 | |
| `mariadb_tmp_table_size`                 | 16M               | |
| `mariadb_users`                          | []                | users to add |
| `mariadb_version`                        | '10.2'            | MariaDB version to install |
| `mariadb_wait_timeout`                   | 28800             | |

## Dependencies

No dependencies

## Example Playbook

```yaml
---
- name: example
  hosts: all
  become: true
  vars:
    mariadb_bind_address: '0.0.0.0'
    mariadb_root_password: 'root'
    mariadb_root_remote: 1
    mariadb_databases:
    - name: dev
    mariadb_users:
    - name: dev
      password: 'devdev'
      priv: "dev.*:ALL"
      host: "%"
  roles:
  - lechuckroh.mariadb     
```

## License
MIT
