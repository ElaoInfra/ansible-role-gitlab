<img src="http://www.elao.com/images/corpo/logo_red_small.png"/>

[![Ansible Role](https://img.shields.io/ansible/role/6902.svg?style=plastic)](https://galaxy.ansible.com/list#/roles/6902) [![Platforms](https://img.shields.io/badge/platforms-debian-lightgrey.svg?style=plastic)](#) [![License](http://img.shields.io/:license-mit-lightgrey.svg?style=plastic)](#)

# Ansible Role: Gitlab

This role will assume the setup of [gitlab community edition](https://about.gitlab.com/)

It's part of the ELAO <a href="http://www.manalas.com" target="_blank">Ansible stack</a> but can be used as a stand alone component.

## Requirements

- Ansible 1.9.0+

## Dependencies

None.

## Installation

Using ansible galaxy:

```bash
ansible-galaxy install elao.gitlab,1.0
```
You can add this role as a dependency for other roles by adding the role to the meta/main.yml file of your own role:

```yaml
dependencies:
  - { role: elao.gitlab }
```

## Role Handlers

| Name                 | Type    | Description                             |
| -------------------- | ------- | --------------------------------------- |
| `gitlab reconfigure` | Service | Reconfigure and restart gitlab services |
| `gitlab restart`     | Service | Restart gitlab services                 |

## Role Variables

| Name                                | Default                           | Type    | Description                                                               |
| ----------------------------------- | --------------------------------  | ------- | ------------------------------------------------------------------------- |
| `elao_gitlab_version`               | ~                                 | String  | Gitlab version to setup. If null, will install the latest stable version. |
| `elao_gitlab_configs`               | []                                | Array   | Configuration files                                                       |
| `elao_gitlab_configs_exclusive`     | false                             | Boolean | If true, will delete any extra configuration files.                       |
| `elao_gitlab_configs_dir`           | /etc/gitlab                       | String  | Path to the main configuration directory.                                 |
| `elao_gitlab_user`                  | root                              | String  | Service and config files owner.                                           |

### Configuration example

```yaml
elao_gitlab_version: 8.1.*

elao_gitlab_configs_exclusive: true
elao_gitlab_configs:
  - file:     gitlab-secrets.json
    template: "{{ playbook_dir }}/templates/gitlab-secrets.json.j2"
  - file:     gitlab.rb
    template: "{{ playbook_dir }}/templates/gitlab.rb.j2"
```

## Example playbook

    - hosts: servers
      roles:
         - { role: elao.gitlab }

# Licence

MIT

# Author information

ELAO [**(http://www.elao.com/)**](http://www.elao.com)
