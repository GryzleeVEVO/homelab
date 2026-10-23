# Pi-hole

Docker Compose project that sets up **Pi-hole**, an ad-blocking DNS sever. It
also has the capability to host DHCP and NTP servers.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.

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
