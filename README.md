# Practical Ansible LDAP

[![CircleCI](https://img.shields.io/circleci/project/github/practical-ansible/ldap.svg)](https://circleci.com/gh/practical-ansible/ldap)
[![Quality](https://img.shields.io/ansible/quality/21425.svg)](https://galaxy.ansible.com/practical-ansible/ldap)
[![Downloads](https://img.shields.io/ansible/role/d/21425.svg)](https://galaxy.ansible.com/practical-ansible/ldap)

Installs Open LDAP (slapd) as service on specified nodes and configures its structure and permissions to identify users and services among multiple domains.

Define `organizations` in your playbook or inventory as array of domains and the role will configure the directory structure for all of them.

You also need to define `base_domain` to keep your passwords stored in password storage.

## Example

```
# playbook.yml
---
- name: Setup LDAP
  hosts: all
  become: yes
  vars:
    base_domain: my.custom.ldap.domain.com
    organizations:
      - example.com

  roles:
    - ldap

```

```
# LDAP Structure
dc=ldap
├─ ou=admin
├─ ou=services
└─ dc=example.com
   ├─ ou=groups
   └─ ou=users
```
