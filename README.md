galaxyproject.miniconda
=======================

An [Ansible][ansible] role for installing and managing [Miniconda][miniconda] installation. Additionally, the role can
manage the creation of a [Conda][conda] environment that can be used to create a [venv][venv] for [Galaxy][galaxy].

[ansible]: https://www.ansible.com/
[miniconda]: https://docs.conda.io/en/latest/miniconda.html
[conda]: https://docs.conda.io/en/latest/
[venv]: https://docs.python.org/3/tutorial/venv.html
[galaxy]: https://galaxyproject.org/

Requirements
------------

A [Conda][conda]-compatible version of Linux or macOS is required.

Role Variables
--------------

See [defaults/main.yml](defaults/main.yml) for a full list.

The only required variable is `miniconda_prefix`, the root of the Conda installation.

To create arbitrary conda environments, use the variable `miniconda_conda_environments` as shown in the defaults, or the
example below. The role will also run `conda install` to update these environments if you change their list of packages
or package versions.

To create an env named `_galaxy_` for creating a venv for [Galaxy][galaxy], set `galaxy_conda_create_env` to `true`. You
can then use `{{ miniconda_prefix }}/envs/_galaxy_/bin/virtualenv` as the value to `galaxy_virtualenv_command` in
[galaxyproject.galaxy][galaxy-role]. This is particularly useful if you need a cross-platform copy of Python and
Galaxy's venv to be deployed on a shared filesystem between a Galaxy server and cluster that may not have matching OS
distributions and versions.

[galaxy-role]: https://github.com/galaxyproject/ansible-galaxy

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: localhost
  vars:
    miniconda_prefix: /conda
    miniconda_conda_environments:
      python@3.9:
        channels:  # optional, defaults to miniconda_channels
          - conda-forge
          - defaults
        packages:
          - python=3.9
  connection: local
  roles:
     - galaxyproject.miniconda
```

License
-------

MIT

Author Information
------------------

[View contributors on GitHub](https://github.com/galaxyproject/ansible-miniconda/graphs/contributors)
