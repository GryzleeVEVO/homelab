# Homelab

Ansible playbooks and Docker Compose projects for managing my homelab: a single
Debian 13 server running media, monitoring and self-hosted services, reachable
from outside through WireGuard.

## Requirements

- `ansible` (the full package, not just `ansible-core`)
- Role and collection dependencies:

  ```bash
  ansible-galaxy install -r requirements.yml
  ```

## Usage

Copy `inventory/inventory_sample.yml` into `inventory/` and fill it in, then run
a playbook:

```bash
ansible-playbook -i inventory/hosts.yml <playbook>.yml [-t <tag>]
```

| Playbook            | Purpose                                                    |
| ------------------- | ---------------------------------------------------------- |
| `postinstall.yml`   | Base system setup: packages, firewall, SSH, Samba, Docker… |
| `home-setup.yml`    | User environment and dotfiles                              |
| `docker-deploy.yml` | Deploy the projects listed in `docker_services`            |
| `vpn.yml`           | WireGuard server and peers                                 |

## Layout

- `roles/`: one role per host service, each documented in its own `README.md`
- `docker/`: one Compose project per directory, templated and deployed to
  `/opt/<project>`
- `inventory/`: hosts and variables (gitignored, except the sample)
