# MOTD role

Role for installing a Message of the Day that shows up on every connection.

## Requirements

`git` required in order to pull [this repo](https://github.com/yboetz/motd).

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
    - motd
```
