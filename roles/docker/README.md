# Docker role

Role for installing Docker, a container runtime.

This role covers:

- Installing Docker.
- Deploying Docker Compose services.

Compose projects are located in the `docker` directory at the root of the
repository.

## Requirements

No requirements.

## Tags

- `docker`: Install Docker.

## Role Variables

No role variables.

## Dependencies

This role depennds on the `geerlingguy.docker` role.

## Example Playbook

### Install `firewalld`

```yaml
- hosts: all
  become: true
  roles:
    - docker
```

### Deploy service

```yaml
- hosts: all
  become: true
  vars:
    service: service_name
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
