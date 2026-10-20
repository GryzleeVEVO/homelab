# Observability stack

Docker Compose project that sets up a services for storing and querying metrics,
logs, and other information from the system and apps.

It consists of:

- **Grafana**: Data visualization frontend.
- **Prometheus**: Time-series database for metrics.
- **Loki**: Logs database.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `grafana_env`: List of envionment variables to pass to Grafana.

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example Playbook

```yaml
- hosts: all
  become: true
  vars:
    service: monitoring
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
