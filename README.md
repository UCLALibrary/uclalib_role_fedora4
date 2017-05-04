# UCLALib Ansible Role: Fedora 4

Deploy a bare-bones installation/configuration of a Fedora 4 repository server.

This role is loosely based on the [Ansible Fedora 4 role created by the Digital Repository of Ireland ](https://github.com/Digital-Repository-of-Ireland/ansible-fedora4).

___This role supports Fedora 4.5.X releases only.___

Deployment documentation is for this version is available at [Deploying Fedora 4 Complete Guide](https://wiki.duraspace.org/x/e4RcB).

Official GitHub repositories are:
* https://github.com/fcrepo4-exts/fcrepo-webapp-plus
* https://github.com/fcrepo4/fcrepo4

The repository you chose depends on the Fedora features you want to enable.

## Dependencies

* uclalib_role_java
* uclalib_role_apache
* uclalib_role_tomcat
* uclalib_role_iptables

## Variables

* `fedora_version` - defines the version of Fedora to use (e.g. 4.0.0, 4.5.0, etc.)

* `fedora_url` - defines the URL to obtain the Fedora WAR file

* `fedora_base` - defines the location of Fedora Tomcat installation directory

* `fedora_home` - defines the location of the Fedora home directory

* `fedora_javaopts` - defines the JVM options to use on Fedora start-up

* `fedora_admin_user` - defines the Fedora admin username

* `fedora_admin_password` - defines the Fedora admin password

## Sample Variable Definition Formats

The variable definitions should be placed in the playbook under the `vars` statement.

If the variable definitions defined in `defaults` are sufficient, your play would look something like:

```ansible
---
- name: uclalib_fedora4test.yml
  sudo: true
  hosts: test
  vars:
    iptables_allowed_input_rules:
      - src_ip: 164.67.0.0/16
        dest_port: 80
        protocol: tcp
    tomcat_applications:
      - app_name: fedora
        shut_port: 8008
        conn_port: 8083
        rproxy_path: fcrepo

    roles:
      - { role: uclalib_role_java }
      - { role: uclalib_role_apache }
      - { role: uclalib_role_tomcat }
      - { role: uclalib_role_solr }
      - { role: uclalib_role_iptables }
```

You can override the defaults by including them in the play:

```ansible
---
- name: uclalib_fedora4test.yml
  sudo: true
  hosts: test
  vars:
    iptables_allowed_input_rules:
      - src_ip: 164.67.0.0/16
        dest_port: 80
        protocol: tcp
    tomcat_applications:
      - app_name: fedora
        shut_port: 8008
        conn_port: 8083
        rproxy_path: fcrepo
    fedora_home: /usr/local/fedora/data
    fedora_javaopts: "-Xms1024m -Xmx2048m -XX:NewSize=256m -XX:MaxNewSize=256m -XX:PermSize=256m -XX:MaxPermSize=256m -XX:+DisableExplicitGC -Dfcrepo.home={{ fedora_home }}/data -Dfcrepo.modeshape.configuration=file://{{ fedora_home }}/etc/modeshape.json"
    fedora_admin_user: adminuser
    fedora_admin_password: password

    roles:
      - { role: uclalib_role_java }
      - { role: uclalib_role_apache }
      - { role: uclalib_role_tomcat }
      - { role: uclalib_role_solr }
      - { role: uclalib_role_iptables }
```
