# Wireguard role

Role for managing a Wireguard peer. Define a set of remote peers and
automatically generate configuration for them.

For the sake of simplicity we'll refer to them as clients, while we'll refer to
the local peer as the server. Although Wireguard is peer-to-peer, in my case I
use it as a tunnel to a server that acts as a router to the rest of the network.

## Requirements

`firewalld` is required in order to open ports and set up forwarding. Otherwise,
the rest of dependencies are handled by using `new_server`. `wg-quick` is used
to set up the tunnels with a `systemd` service.

## Tags

- `new_server`: Set up the local peer.
- `add_clients`: Add remote peers as specified in `wireguard_clients`. You
    should run `new_server` at least once before adding any clent.
- `remove_clients`: Detect and remove any client that is not listed in
    `wireguard_clients`.

## Role Variables

- `wireguard_server_ip`: Private IP of the local peer.
- `wireguard_server_public_endpoint`: Public IP of the local peer.
- `wireguard_clients`: List of peers to configure.

Check [`meta/argument_specs.yml`](./meta/argument_specs.yml) for the complete
schema.

The following optional variables are available:

- `rotate_server` (Optional): Rotate the key pairs from local peer before
    generating the configuration.
- `rotate_all` (Optional): Rotate the key pairs for all remote peers.
- `rotate_clients` (Optional): Rotate the specified clients from a
    comma-separated list. E.g. `rotate_clients: laptop,phone`

For other optional variables, check [`defaults/main.yml`](./defaults/main.yml).

## Dependencies

It is recommended to run the `firewalld` role first in order to set up a
firewall.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - wireguard
```
