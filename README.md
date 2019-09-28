omsagent
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-omsagent"><img src="https://travis-ci.org/robertdebock/ansible-role-omsagent.svg?branch=master" alt="Build status" align="left"/></a>

Install Microsoft omsagent (Log Analytics agent) on your system.

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
    - robertdebock.omsagent
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
    - role: robertdebock.users
      users_group_list:
        - name: omiusers
      users_user_list:
        - name: omsagent
          group: omiusers
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for omsagent
# Extra documentation on Log Analytic Agent is available on:
# https://docs.microsoft.com/en-us/azure/azure-monitor/platfrom/logs-analytics-agent

omsagent_version: 1.11.0-9

# omsagent_tmp directory is where the installer script is placed.
# The installer downloads a large file (125MB) to this directory.
omsagent_tmp: /tmp

# Set the user and group owning the directory.
omsagent_owner: omsagent
omsagent_group: omiusers

# Use workspace ID for automatic onboarding.
omsagent_id: []

# Use as the shared key for automatic onboarding.
omsagent_shared_key: []

# Use as the OMS domain for onboarding.
# For azure monitoring log Analytics workspace in Goverment cloud use:
# omsagent_domain: opinsights.azure.command
# leave emapy to use scripts default (omsagent_domain: opinsights.azure.com).
omsagent_domain: []

# Use [protocol://][user:password@]proxyhost[:port] as the proxy configuration.
# omsagent_proxy: "https://username:password@proxyserver:proxyport"
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.users

```

This role uses the following modules:
```yaml
---
- command
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
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/omsagent.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.7|ansible 2.8|ansible devel|
|------------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes*|
|alpine-latest|yes|yes|yes*|
|archlinux|yes|yes|yes*|
|centos-6|yes|yes|yes*|
|centos-latest|yes|yes|yes*|
|debian-stable|yes|yes|yes*|
|debian-unstable*|yes|yes|yes*|
|fedora-latest|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes*|
|opensuse-leap|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes*|
|ubuntu-rolling|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.




Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-omsagent) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-omsagent/issues)

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
