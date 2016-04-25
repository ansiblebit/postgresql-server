# PostgreSQL server

[![License](https://img.shields.io/badge/license-New%20BSD-blue.svg?style=flat)](https://raw.githubusercontent.com/ansiblebit/postgresql/master/LICENSE)

[![Platform](http://img.shields.io/badge/platform-macosx-000000.svg?style=flat)](#)

[![Project Stats](https://www.openhub.net/p/ansiblebit-postgresql/widgets/project_thin_badge.gif)](https://www.openhub.net/p/ansiblebit-postgresql/)

Ansile role to setup [PostgreSQL][postgresql] server on OSX.

This role will install the [PostgreSQL][postgresql] version that comes with [macports][macports].


## Tests

| Family | Distribution | Version | Test Status |
|:-:|:-:|:-:|:-:|
| Darwin | MacOSX  | 10.11  | [![x86_64](http://img.shields.io/badge/x86_64-passed-006400.svg?style=flat)](#) |


## Requirements

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here.
For instance, if the role uses the EC2 module,
it may be a good idea to mention in this section that the boto package is required.

- ansible >= 1.9.4
- [ansiblebit/macports][ansiblebit.macports]


## Role Variables

- **postgresql_set_default: flag to indicate if the current version should be set as default.
- **postgresql_users: a list of users to setup their environment with PostgreSQL aliases.
- **postgresql_version**: the PostgreSQL version to be installed (major and minor version number must be specified).


## Playbooks

    ---

    - name: PostgreSQL play
      hosts: "{{ vagrant_box }}"
      gather_facts: yes
      vars:
        debug: yes

        macports_selfupdate: no
        macports_upgrade_outdated: no

        postgresql_version: 9.5
        postgresql_set_default: yes
        postgresql_users:
          - steenzout


      roles:
        - role: postgresql_server
          tags: [ database, postgresql, server ]

        - role: tests
          tags: test


## Tags

- **configuration**: configuration tasks.
- **debug**: task to debug role variables.
- **installation**: installation tasks.
- **validation**: task to validate role variables.


## Test

To run the tests you will need to install:

- [tox](https://tox.readthedocs.org/)
- [vagrant](https://www.vagrantup.com/)

To run all tests against all pre-defined OS/distributions * ansible versions:

```
$ tox
```

To run tests for `trusty64`:

```
$ cd tests
$ bash test_idempotence.sh --box trusty64.vagrant.dev
# log file will be stores under tests/log
```

To perform debugging on a specific environment:

```
$ cd tests
$ vagrant up trusty64.vagrant.dev

# to provision using the test.yml playbook (as many time as you need)
$ vagrant provision trusty64.vagrant.dev

# to access the Vagrant box
$ vagrant ssh trusty64.vagrant.dev
```


## Links

- [PostgreSQL homepage][postgresql]


## License

[BSD][license]


## Author Information

- [steenzout][steenzout]


[ansiblebit.macports]:   https://github.com/ansiblebit/macports/    "ansiblebit/macports"
[license]:      https://raw.githubusercontent.com/ansiblebit/postgresql/master/LICENSE  "License"
[macports]:     https://macports.org/           "macports.org"
[postgresql]:   http://postgresql.org/          "PostgreSQL"
[steenzout]:    https://github.com/steenzout/   "steenzout"
