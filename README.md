# [owncloud](#owncloud)

Install and configure owncloud on your system.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-owncloud/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-owncloud/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-owncloud/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-owncloud)|[![quality](https://img.shields.io/ansible/quality/58028)](https://galaxy.ansible.com/buluma/owncloud)|[![downloads](https://img.shields.io/ansible/role/d/58028)](https://galaxy.ansible.com/buluma/owncloud)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-owncloud.svg)](https://github.com/buluma/ansible-role-owncloud/pulls/)|

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

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Build Status GitHub](https://github.com/buluma/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-buildtools/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-buildtools)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.cron](https://galaxy.ansible.com/buluma/cron)|[![Build Status GitHub](https://github.com/buluma/ansible-role-cron/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-cron/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-cron/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-cron)|
|[buluma.epel](https://galaxy.ansible.com/buluma/epel)|[![Build Status GitHub](https://github.com/buluma/ansible-role-epel/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-epel/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-epel/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-epel)|
|[buluma.httpd](https://galaxy.ansible.com/buluma/httpd)|[![Build Status GitHub](https://github.com/buluma/ansible-role-httpd/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-httpd/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-httpd/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-httpd)|
|[buluma.mysql](https://galaxy.ansible.com/buluma/mysql)|[![Build Status GitHub](https://github.com/buluma/ansible-role-mysql/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-mysql/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-mysql/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-mysql)|
|[buluma.openssl](https://galaxy.ansible.com/buluma/openssl)|[![Build Status GitHub](https://github.com/buluma/ansible-role-openssl/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-openssl/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-openssl/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-openssl)|
|[buluma.php](https://galaxy.ansible.com/buluma/php)|[![Build Status GitHub](https://github.com/buluma/ansible-role-php/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-php/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-php/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-php)|
|[buluma.php_fpm](https://galaxy.ansible.com/buluma/php_fpm)|[![Build Status GitHub](https://github.com/buluma/ansible-role-php_fpm/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-php_fpm/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-php_fpm/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-php_fpm)|
|[buluma.python_pip](https://galaxy.ansible.com/buluma/python_pip)|[![Build Status GitHub](https://github.com/buluma/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-python_pip/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-python_pip)|
|[buluma.redis](https://galaxy.ansible.com/buluma/redis)|[![Build Status GitHub](https://github.com/buluma/ansible-role-redis/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-redis/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-redis/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-redis)|
|[buluma.remi](https://galaxy.ansible.com/buluma/remi)|[![Build Status GitHub](https://github.com/buluma/ansible-role-remi/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-remi/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-remi/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-remi)|
|[buluma.selinux](https://galaxy.ansible.com/buluma/selinux)|[![Build Status GitHub](https://github.com/buluma/ansible-role-selinux/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-selinux/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-selinux/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-selinux)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-owncloud/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|bullseye|
|[opensuse](https://hub.docker.com/repository/docker/buluma/opensuse/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|focal|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-owncloud/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-owncloud/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-owncloud/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

Please consider [sponsoring me](https://github.com/sponsors/buluma).

### [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
