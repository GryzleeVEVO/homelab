# Homepage

Docker Compose project that sets up a simple homepage app.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `homepage_services`: Dictionary of services to configure.
- `homepage_openmeteo_data`: Set up location for the weather widget.

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example playbook

```yaml
- hosts: all
  become: true
  vars:
    service: homepage
  tasks:
    - name: Deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
