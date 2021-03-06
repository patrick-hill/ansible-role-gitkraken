Ansible Role: GitKraken
=======================

[![Build Status](https://travis-ci.org/gantsign/ansible-role-gitkraken.svg?branch=master)](https://travis-ci.org/gantsign/ansible-role-gitkraken)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gantsign.gitkraken-blue.svg)](https://galaxy.ansible.com/gantsign/gitkraken)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gantsign/ansible-role-gitkraken/master/LICENSE)

Role to download and install the [GitKraken](https://www.gitkraken.com) Git client.

Requirements
------------

* Ansible

    * Minimum 2.0
    * Maximum 2.3 (currently using `always_run`, which is scheduled for removal
      in 2.4)

* Ubuntu

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# The download URL for the redistributable package
gitkraken_redis_url: https://release.gitkraken.com/linux/gitkraken-amd64.deb

# Directory to store files downloaded for GitKraken installation
gitkraken_download_dir: "{{ x_ansible_download_dir | default('~/.ansible/tmp/downloads') }}"

# Should the config dir be replaced with a symlink to a backup directory
gitkraken_backup_use_symlink: false

# Directory of source dir to symlink to ~/.gitkraken
gitkraken_backup_src_dir: '' # Must be defined to use & above boolean must be set to true

# Default way to detect the home directory for use with the backup directory
# This is not ideal as this will report the user that Ansible is running as
os_username: "{{ lookup('env','USER') }}"
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - { role: gantsign.gitkraken }
```
```yaml
- hosts: servers
  vars:
    - os_username: myUserName
    - gitkraken_backup_use_symlink: true
    - gitkraken_backup_src_dir: /path/to/your/backup/dir
  roles:
     - { role: gantsign.gitkraken }
```   

More Roles From GantSign
------------------------

You can find more roles from GantSign on
[Ansible Galaxy](https://galaxy.ansible.com/gantsign).

Development & Testing
---------------------

This project uses [Molecule](http://molecule.readthedocs.io/) to aid in the
development and testing; the role is unit tested using
[Testinfra](http://testinfra.readthedocs.io/) and
[pytest](http://docs.pytest.org/).

To develop or test you'll need to have installed the following:

* Linux (e.g. [Ubuntu](http://www.ubuntu.com/))
* [Docker](https://www.docker.com/)
* [Python](https://www.python.org/) (including python-pip)
* [Ansible](https://www.ansible.com/)
* [Molecule](http://molecule.readthedocs.io/)

To run the role (i.e. the `tests/test.yml` playbook), and test the results
(`tests/test_role.py`), execute the following command from the project root
(i.e. the directory with `molecule.yml` in it):

```bash
molecule test
```

License
-------

MIT

Author Information
------------------

John Freeman

GantSign Ltd.
Company No. 06109112 (registered in England)
