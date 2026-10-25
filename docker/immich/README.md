# Immich

Docker Compose project that sets up **Immich**, a self-hosted photo and video
management system similar to Google Photos.

It consist of four components:

- The **server** itself.
- A **machine learning** process for semantic search of photos and face
    recognition.
- A **Valkey** (Redis) cache.
- A **Postgres** database with extra extensions for retrieval via vector search.

## Requirements

**Docker** is required to be installed. It can be installed using the `docker`
role.

## Tags

No tags exist for this project.

## Variables

- `version_tags`: Dictionary with the versions for each service.
- `photos_directory`: Path to the photos directory.
- `immich_pg_password`: Password for the Postgres database.

## Dependencies

The `docker` task must be run at least once before running the playbook.

## Example playbook

```yaml
- hosts: all
  become: true
  vars:
    service: immich
  tasks:
    - name: deploy service
      ansible.builtin.import_role:
        name: docker
        tasks_from: deploy.yml
```
