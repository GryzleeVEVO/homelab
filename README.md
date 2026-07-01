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

## Homelab overview

The setup currently consists of a single PC (hostname: `ubermaquinita`) with
the following specs:

- CPU: Intel i5 6400 @2.7 GHz
- GPU: Intel HD Grahpics 530 integrated card
- RAM: 8GB RAM DDR4 @2100 MT/s
- Storage:
    - 120G Emtec X150
    - 4TB Seagate Ironwolf Pro (ST4000NT001-3M2101)
    - 1TB Seagate Barracuda (ST1000DM003-1SB102)

**Debian 13** is used as the operating system.

### Infrastructure

**firewalld** is used as the firewall daemon. It is chosen mostly for the
(mostly) seamless interop with Docker's runtime firewall rules.

**unattended-upgrades** is installed and running in order to automatically
update packages while running.

An instance of **Pi-hole** runs on Docker and is used as the default DNS for
the system and the VPN.

### Mediaserver

The media setup consist of:

- **Jellyfin** for browsing and playing back media
- The **arr* stack for fetching new media:
    - **Radarr** for movies
    - **Sonarr** for shows
    - **Lidarr** for music
    - **Prowlarr** as a index manager for all of the above
    - A **Qbittorrent** client for downloads

All services are run through Docker.

### Observability

Instances of **Grafana**, **Prometheus** and **Loki** run on Docker.

- **Prometheus** is a time-series database for metrics
- **Loki** is a logs database
- **Grafana** is a monitoring frontend that integrates with these two.

Aditionally, the following are installed on the host:

- **node_exporter** for exposing system metrics to Prometheus.
- **Alloy** for collecting and sending logs to Loki.

### Wireguard

Wireguard is used as a VPN, in order to be able to connect remotely and securely
to the host from outside the network.

Although Wireguard is peer-to-peer, the homelab acts as the only gateway for all
peers, so it is more of a client-server setup with the lab acting as a router to
the internal network.

### WOL

The built-in NIC (Killer E2400) by default has broken Wake-on-LAN funcionality.
[This repo](https://github.com/AndiWeiss/alx-wol) provides a DKMS module that
restores the funcionality and fixes the bugs that caused for WOL being disabled
by default (mostly, it still resets when the router restarts for an update).
