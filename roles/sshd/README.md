# SSH role

Role for setting up the SSH daemon on new hosts.

## Requirements

`openssh` or other SSH server should be installed by default in most distros.

## Tags

No tags exist for this role.

## Role Variables

- `sshd_no_password`: Disable password-based authentication. The connection
    to the host must be made using key-based authentication, otherwise it
    takes no effect.

## Dependencies

No dependencies from other roles.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - ssh
```
