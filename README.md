# Practical Ansible LDAP

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
