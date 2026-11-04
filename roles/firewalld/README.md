# Firewalld role

Role for installing and managing Firewalld, a zones-based stateful firewall.

This role covers:

- Installing `firewalld`.
- Configuring each service in their own file.

## Requirements

No requirements.

## Tags

- `firewalld`: Install firewalld

## Role Variables

No role variables.

## Dependencies

The `ansible.posix` collection is required. It should come bundled with
most Ansible distributions.

## Example Playbook

### Install `firewalld`

```yaml
- hosts: all
  become: true
  roles:
    - firewalld
```

### Open ports for a service

```yaml
- hosts: all
  become: true
  tasks:
    - name: Open ports for foobar
      import_role:
        name: firewalld
        tasks_from: foobar
```
