# VPN setup guide

## Prerequisites

Run the postinstall with the option to disable password authentication to the
VPN host.

## Playbook

Run `playbooks/vpn.yml`. There are three tags:

- `new_server`: Set up a new interface `wg0`.
- `add_clients`: Set up clients from `wireguard_clients`.
- `remove_clients`: Remove clients not present in `wireguard_clients`.
