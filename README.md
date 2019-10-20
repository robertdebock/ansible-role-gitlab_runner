gitlab_runner
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-gitlab_runner"><img src="https://travis-ci.org/robertdebock/ansible-role-gitlab_runner.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure gitlab-runner on your system.

<img src="https://img.shields.io/ansible/role/d/40614"/>
<img src="https://img.shields.io/ansible/quality/40614"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.gitlab_runner
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Converge
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

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

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

Requirements
------------

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

This role uses the following modules:
```yaml
---
- command
- expect
- file
- get_url
- package
- service
- template
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/gitlab_runner.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|allow_failures|
|---------|--------------|
|docker-alpine-openrc|yes|
|docker-alpine-openrc|yes|
|docker-centos-systemd|no|
|docker-centos-systemd|no|
|docker-debian-systemd|yes|
|docker-debian-systemd|yes|
|docker-debian-systemd|yes|
|docker-fedora-systemd|yes|
|docker-fedora-systemd|yes|
|opensuse/|no|
|docker-ubuntu-systemd|yes|
|docker-ubuntu-systemd|yes|
|docker-ubuntu-systemd|yes|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.5.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Archlinux | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| CentOS 8 | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Fedora | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |
| Ubuntu rolling | Not supported, see https://docs.gitlab.com/ee/install/requirements.html |



Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-gitlab_runner) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-gitlab_runner/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
