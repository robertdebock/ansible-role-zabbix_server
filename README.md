# [zabbix_server](#zabbix_server)

Install and configure zabbix_server on your system.

|Travis|GitHub|GitLab|Quality|Downloads|Version|
|------|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-zabbix_server.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-zabbix_server)|[![github](https://github.com/robertdebock/ansible-role-zabbix_server/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-zabbix_server/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-zabbix_server/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-zabbix_server)|[![quality](https://img.shields.io/ansible/quality/35783)](https://galaxy.ansible.com/robertdebock/zabbix_server)|[![downloads](https://img.shields.io/ansible/role/d/35783)](https://galaxy.ansible.com/robertdebock/zabbix_server)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-zabbix_server.svg)](https://github.com/robertdebock/ansible-role-zabbix_server/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.zabbix_server
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.selinux
    - role: robertdebock.container_docs
    - role: robertdebock.mysql
      mysql_databases:
        - name: zabbix
          encoding: utf8
          collation: utf8_bin
      mysql_users:
        - name: zabbix
          password: zabbix
          priv: "zabbix.*:ALL"
    - role: robertdebock.zabbix_repository
    - role: robertdebock.core_dependencies
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for zabbix_server

# The details to connect to the database.
zabbix_server_database_name: zabbix
zabbix_server_database_user: zabbix
zabbix_server_database_password: zabbix

# How to connect to the mysql database, either `socket` or `network`.
zabbix_server_mysql_connection: socket

# When `zabbix_server_mysql_connection` is set to `network` this role needs
# these three extra setting.
# zabbix_server_database_host: localhost
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-zabbix_server/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |
| [robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-core_dependencies.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-core_dependencies) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions) |
| [robertdebock.container_docs](https://galaxy.ansible.com/robertdebock/container_docs) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-container_docs.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-container_docs) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-container_docs/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-container_docs/actions) |
| [robertdebock.mysql](https://galaxy.ansible.com/robertdebock/mysql) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-mysql.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-mysql) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-mysql/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-mysql/actions) |
| [robertdebock.selinux](https://galaxy.ansible.com/robertdebock/selinux) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-selinux.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-selinux) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-selinux/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-selinux/actions) |
| [robertdebock.zabbix_repository](https://galaxy.ansible.com/robertdebock/zabbix_repository) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-zabbix_repository.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-zabbix_repository) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-zabbix_repository/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-zabbix_repository/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-zabbix_server/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|opensuse|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| amazonlinux | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Archlinux | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| CentOS 8 | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Debian | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Fedora | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| openSUSE | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Ubuntu rolling | Zabbix has [limited OS support](https://www.zabbix.com/download). |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-zabbix_server) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-zabbix_server/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
