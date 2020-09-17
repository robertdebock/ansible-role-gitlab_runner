# [gitlab_runner](#gitlab_runner)

Install and configure gitlab-runner on your system.

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-gitlab_runner.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-gitlab_runner)|[![github](https://github.com/robertdebock/ansible-role-gitlab_runner/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-gitlab_runner/actions)|[![quality](https://img.shields.io/ansible/quality/40614)](https://galaxy.ansible.com/robertdebock/gitlab_runner)|[![downloads](https://img.shields.io/ansible/role/d/40614)](https://galaxy.ansible.com/robertdebock/gitlab_runner)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-gitlab_runner.svg)](https://github.com/robertdebock/ansible-role-gitlab_runner/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.gitlab_runner
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.python_pip
      python_pip_modules:
        - name: pexpect
```

For verification `molecule/resources/verify.yml` runs after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: no

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for gitlab_runner

# These are the setting you need to register a runner.
# gitlab_runner_token: 123ABC
# gitlab_runner_url: http://localhost/
# gitlab_runner_description: My GitLab Runner
# gitlab_runner_tags: "docker,my_runner"
# gitlab_runner_executor: docker
gitlab_runner_docker_image: "alpine:latest"

gitlab_runner_home_directory: /home/gitlab-runner
gitlab_runner_config: /etc/gitlab-runner/config.toml
gitlab_runner_service: gitlab-runner
gitlab_runner_user: gitlab-runner
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/gitlab_runner.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Archlinux | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| EL 8 | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Fedora | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Ubuntu rolling | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| debian:buster | Not supported, see https://docs.gitlab.com/runner/install/linux-repository.html |


## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-gitlab_runner) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-gitlab_runner/issues)

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

## [Contributors](#contributors)

I'd like to thank everybody that made contributions to this repository. It motivates me, improves the code and is just fun to collaborate.

- [dbenaben](https://github.com/dbenaben)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
