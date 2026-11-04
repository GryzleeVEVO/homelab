# `unattended-upgrades` role

Role for installing `unattended-upgrades`, which upgrades the system without
user intervention periodically.

## Requirements

`unattended-upgrades` is available only on Debian-based distros.

## Tags

No tags exist for this role.

## Role Variables

No variables exist for this role.

## Dependencies

No dependencies from other roles.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - wol
```
