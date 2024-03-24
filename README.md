# Ansible role [owncloud](https://galaxy.ansible.com/ui/standalone/roles/buluma/owncloud/documentation)

Install and configure owncloud on your system.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-owncloud/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-owncloud/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/owncloud)](https://galaxy.ansible.com/ui/standalone/roles/buluma/owncloud/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-owncloud/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: buluma.owncloud
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-owncloud/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.bootstrap
    - role: buluma.core_dependencies
    - role: buluma.cron
    - role: buluma.buildtools
    - role: buluma.epel
    - role: buluma.python_pip
    - role: buluma.openssl
      openssl_items:
        - name: apache-httpd
          common_name: "{{ ansible_fqdn }}"
    - role: buluma.selinux
    - role: buluma.httpd
    - role: buluma.redis
    - role: buluma.remi
      remi_enabled_repositories:
        - php73
      when:
        - ansible_distribution != "Fedora"
    - role: buluma.php
    - role: buluma.php_fpm
    - role: buluma.mysql
      mysql_databases:
        - name: owncloud
          encoding: utf8
          collation: utf8_bin
      mysql_users:
        - name: owncloud
          password: 0wnCl0uD
          priv: "owncloud.*:ALL"
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-owncloud/blob/master/defaults/main.yml):

```yaml
---
# defaults file for owncloud

# The version of owncloud to install.
owncloud_version: "10.11.0"

# The domain under which this server will be available. For example:
# "localhost" or "owncloud.example.com". Does not include protocol identifier,
# (https://) or directories. (/owncloud)
owncloud_domain_url: "{{ ansible_default_ipv4.address | default(ansible_all_ipv4_addresses[0]) }}"

# Database connection details.
owncloud_database_name: owncloud
owncloud_database_user: owncloud
owncloud_database_pass: 0wnCl0uD
owncloud_database_host: "127.0.0.1"
owncloud_admin_user: admin
owncloud_admin_pass: OwnCl0uD
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-owncloud/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Ansible Molecule](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-buildtools.svg)](https://github.com/shadowwalker/ansible-role-buildtools)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Ansible Molecule](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-core_dependencies.svg)](https://github.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.cron](https://galaxy.ansible.com/buluma/cron)|[![Ansible Molecule](https://github.com/buluma/ansible-role-cron/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-cron/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-cron.svg)](https://github.com/shadowwalker/ansible-role-cron)|
|[buluma.epel](https://galaxy.ansible.com/buluma/epel)|[![Ansible Molecule](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-epel.svg)](https://github.com/shadowwalker/ansible-role-epel)|
|[buluma.httpd](https://galaxy.ansible.com/buluma/httpd)|[![Ansible Molecule](https://github.com/buluma/ansible-role-httpd/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-httpd/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-httpd.svg)](https://github.com/shadowwalker/ansible-role-httpd)|
|[buluma.mysql](https://galaxy.ansible.com/buluma/mysql)|[![Ansible Molecule](https://github.com/buluma/ansible-role-mysql/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-mysql/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-mysql.svg)](https://github.com/shadowwalker/ansible-role-mysql)|
|[buluma.openssl](https://galaxy.ansible.com/buluma/openssl)|[![Ansible Molecule](https://github.com/buluma/ansible-role-openssl/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-openssl/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-openssl.svg)](https://github.com/shadowwalker/ansible-role-openssl)|
|[buluma.php](https://galaxy.ansible.com/buluma/php)|[![Ansible Molecule](https://github.com/buluma/ansible-role-php/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-php/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-php.svg)](https://github.com/shadowwalker/ansible-role-php)|
|[buluma.php_fpm](https://galaxy.ansible.com/buluma/php_fpm)|[![Ansible Molecule](https://github.com/buluma/ansible-role-php_fpm/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-php_fpm/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-php_fpm.svg)](https://github.com/shadowwalker/ansible-role-php_fpm)|
|[buluma.python_pip](https://galaxy.ansible.com/buluma/python_pip)|[![Ansible Molecule](https://github.com/buluma/ansible-role-python_pip/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-python_pip/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-python_pip.svg)](https://github.com/shadowwalker/ansible-role-python_pip)|
|[buluma.redis](https://galaxy.ansible.com/buluma/redis)|[![Ansible Molecule](https://github.com/buluma/ansible-role-redis/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-redis/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-redis.svg)](https://github.com/shadowwalker/ansible-role-redis)|
|[buluma.remi](https://galaxy.ansible.com/buluma/remi)|[![Ansible Molecule](https://github.com/buluma/ansible-role-remi/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-remi/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-remi.svg)](https://github.com/shadowwalker/ansible-role-remi)|
|[buluma.selinux](https://galaxy.ansible.com/buluma/selinux)|[![Ansible Molecule](https://github.com/buluma/ansible-role-selinux/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-selinux/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-selinux.svg)](https://github.com/shadowwalker/ansible-role-selinux)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-owncloud/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Debian](https://hub.docker.com/r/buluma/debian)|bullseye|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|focal|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-owncloud/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-owncloud/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-owncloud/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)

