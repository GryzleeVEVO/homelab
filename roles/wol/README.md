# WOL role

Role for enabling and setting up Wake-on-LAN capabilities. This allows a remote
user to wake up a host by sending magic packets, and suspend it via SSH and a
set of restricted commands in order to save energy.

## Requirements

The host must allow for password authentication in order to remotely suspend
a host using [this Android app](https://github.com/Florianisme/WakeOnLan).

## Tags

No tags exist for this role.

## Role Variables

- `wol_remote_user`: Name of user which will send suspend requests via SSH. This
    will install a sudoer file allowing passwordless shutdowns and suspends.
- `wol_interface`: Name of the interface on which to enable Wake-on-LAN.
- `wol_alx`: Set this variable to true in order to install this [patched kernel
    module](https://github.com/AndiWeiss/alx-wol) for Qualcomm Atheros/Killer
    NICs. WoL capabilities were removed due to a bug that was not upstreamed
    into the kernel. This patch re-enables it while fixing the bug.

## Dependencies

No dependencies from other roles.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - wol
```
