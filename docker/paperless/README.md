# Paperless

Docker Compose project that sets up **Paperless NGX**, a document
management app.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `paperless_pg_password`: Password for the Postgres database
- `paperless_secret_key`: API key

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
    service: paperless
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
