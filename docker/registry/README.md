# Docker Registry

Docker Compose project that sets up a **Docker Registry**, alongside a web UI
for looking up uploaded images.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `docker_registry_ui_env`: Extra environment variables for the Docker Registry.
    Required for enabling the web UI as a remote origin for CORS.

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
    service: pihole
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
