# Homelab

This repository contains a series of playbooks I use to manage my homelab.

## Features

- Set up a newly installed system and your user
- Install and set up apps and services
- Set up and deploy Docker Compose projects
- Set up a VPN, and create peers from a list

## Requirements

Install `ansible`. Since some of the `ansible.*` and `community.*` modules are
used, it is recommended to install the full version instead of just
`ansible-core`.

In order to install dependencies for the roles:

```bash
ansible-galaxy install -r requirements.yml
```

## Usage

Create an inventory and run any of the playbooks in the project root.

E.g.

```bash
ansible-playbook -i inventory/servers.yml postinstall.yml -t nginx
```

For more in-depth guides, follow the guides in `docs`.
