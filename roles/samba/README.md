# Samba role

Role for setting up a standalone SMB server. SMB is Windows' file-sharing
protocol, widely compatible with many devices.

## Requirements

No requirements needed.

## Tags

No tags.

## Role variables

- `samba_shares`: A dictionary of shares with the following format:

```yaml
samba_shares:
    - name: share_name
      path: /srv/media
      readonly: false
      browseable: true
```

## Dependencies

No hard depencencies required. It is recommended to run `firewalld` in order
to filter ports.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - samba
```
