# Home setup

## Prerequisites

It is recommended to run (`postinstall.yml`)[./postinstall.md] before running this playbook.

## Run playbook

This playbook will:

- Install some basic packages
- Set up directories
- Clone and install dotfiles with `stow`
- Generate or regenerate SSH keys

```bash
# Comma in ad-hoc hosts mandatory
# SSH and sudo password with -kK
ansible-playbook -kK -i <host_ip_1>,... playbooks/home-setup.yml
```

### Extra variables (-e)

- *regenerate_keys*: Regenerate SSH keys even if present
