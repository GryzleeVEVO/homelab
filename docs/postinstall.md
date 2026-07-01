# Post install guide

## Prerequisites

After installing Debian, `sudo` must be installed and the user added to the `sudo` group.

```bash
# If not logged in from getty, log in as root with su
su -

apt update
apt install sudo

usermod -aG sudo <username>
```

When disabling password authentication for SSH, keys must be copied beforehand. There are
safeguards in order to avoid being locked out:

```bash
ssh-copy-id <host_ip>
```

You may need to pull Ansible Galaxy dependencies

```bash
ansible-galaxy install -r playbooks/requirements.yml
```

## Run playbook

This playbook will:

- Install some basic packages
- Change the hostname to a user-defined one
- Set up SSH and a firewall with firewalld
- Install other software (see tags)

```bash
# Comma in ad-hoc hosts mandatory
# SSH and sudo password with -kK
ansible-playbook -kK -i <host_ip_1>,... playbooks/postinstall.yml
```

### Tags (-t)

- prerequisites: Install basic packages and change the hostname if necessary
- sshd
- firewalld
- wol: Fix for Atheros NICs to enable WOL
- node_exporter: Export system metrics
- plocate: Keep a file index for quick lookup
- unattended-upgrades: Update packages without intervention
- docker: Container runtime

### Extra variables (-e)

- *hostname*: New hostname. Defaults to "base".
- *sshd_no_password*: If set, password authentication will be disabled.
- *wol_remote_user*: Set the remote user that will be able to shut down and suspend the PVE remotely.

## Home setup

Use [`home-setup.yml`](./home-setup.md) to set up the base user
