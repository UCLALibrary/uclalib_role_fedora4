# UCLALib Ansible Role: Fedora 4

Ansible role to install and configure the Fedora repository application on a RHEL system using MySQL for the back-end.

Deploy a bare-bones installation/configuration of a Fedora 4 repository server.

___This role supports Fedora 4.7.X releases only.___

Deployment documentation is for this version is available at [Deploying Fedora 4 Complete Guide](https://wiki.duraspace.org/x/PjdsBQ).

Official GitHub repository:
* https://github.com/fcrepo4-exts/fcrepo-webapp-plus
* https://github.com/fcrepo4/fcrepo4

## Requirements

It is assumed a MySQL server is installed, configured, and running in some location (local or remote) for this instance of Fedora use.

A fedora database and user also needs to have already been created within MySQL.

## Dependencies

* uclalib_role_java
* uclalib_role_apache
* uclalib_role_tomcat

## Variables

* `fedora_version` - defines the version of Fedora to use (e.g. 4.0.0, 4.5.0, etc.)

* `fedora_url` - defines the URL to obtain the Fedora WAR file

* `fedora_base_dir` - defines the location of Fedora Tomcat installation directory

* `fedora_tomcat_user` - defines the tomcat user fedora will run as

* `fedora_min_mem` -  defines the fedora/tomcat minimum memory allocation

* `Fedora_max_mem` - defines the fedora/tomcat maximum memory allocation

* `fedora_data_dir` - defines the location of the Fedora data directory

* `fedora_db_user` - defines the user fedora will use to connect to the database

* `fedora_db_password` - defines the password fedora will use to connect to the database

* `fedora_db_host` - defines the FQDN of the database server

* `fedora_db_port` - defines the network port for connecting to the database

* `fedora_db_name` - defines the name of the fedora database

* `fedora_config_dir` - defines the path to the external fedora configuration directory

* `fedora_log_dir` - defines the path to the fedora log directory

* `fedora_admin_user` - defines the Fedora admin username

* `fedora_admin_password` - defines the Fedora admin password

## Sample Variable Definition Formats

The variable definitions should be placed in the playbook under the `vars` statement.

You can override the defaults by including them in a playbook:

```
---
- name: uclalib_fedora4test.yml
  sudo: true
  hosts: test
  vars:
    tomcat_applications:
      - app_name: fedora
        shut_port: 8008
        conn_port: 8083
        rproxy_path: fcrepo
    fedora_home: /opt/fedora-data
    fedora_db_user: fedorauser
    fedora_db_password: resuarodef
    fedora_db_host: mysqlhost.library.ucla.edu
    fedora_db_name: fedoratest
    fedora_admin_user: adminuser
    fedora_admin_password: password

    roles:
      - { role: uclalib_role_java, oracle_java_version: '1.8.0_181' }
      - { role: uclalib_role_apache }
      - { role: uclalib_role_tomcat }
      - { role: uclalib_role_fedora4 }
```
