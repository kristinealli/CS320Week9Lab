# VyOS Network Management

Ansible project for gathering facts and managing a VyOS router over its network
CLI. The inventory and playbook currently target the VyOS group and configure a
hostname, a DMZ VLAN interface, OSPF, a login banner, and an ICMP firewall rule.

## Project files

- `inventory.ini` — VyOS host, connection type, and network OS settings.
- `network_management.yml` — configuration and verification tasks.
- `requirements.yml` — Ansible collections used by the project.
- `group_vars/` — group variables, which may contain Ansible Vault-encrypted
  credentials.
- `evidence/` — local command output; generated `.log` files are ignored by Git.

## Requirements

- WSL with Python 3 and Ansible installed.
- The `ansible.netcommon` and `vyos.vyos` collections.
- Network access from WSL to the router at `10.2.37.40`.
- Credentials for the VyOS SSH account. If credentials are stored in an
  encrypted vars file, the Ansible Vault password is also required.

Ansible can use Paramiko for its SSH transport. If Ansible reports that
`ansible-pylibssh` is unavailable and falls back to Paramiko, that warning is
informational as long as Paramiko is installed and the connection proceeds.

## Install collections

From this directory in WSL:

```bash
ansible-galaxy collection install -r requirements.yml
```

## Run Playbook

From this directory in WSL:

```bash
ansible-playbook -i inventory.ini network_management.yml --ask-vault-pass
```
You will be prompted for the vault password.

The `.gitignore` rules exclude generated evidence logs and local credential
files. Keep passwords and private keys out of unencrypted files and logs.
