# Oracle 19c Data Guard Ansible Automation

Ansible playbooks and roles for automating Oracle 19c Physical Standby Data Guard in a non-CDB environment. Covers software preparation, installation, primary DB creation, standby config, replication testing, and Data Guard Broker enablement.

## Overview
- **Roles**:
  - `oracle_install`: Handles Oracle binaries, dirs, and primary DB.
  - `oracle_dataguard`: DG-specific config, duplication, and testing.
- **Playbooks**:
  - `oracle_dg_setup.yml`: Installs on primary, configures DG on all.
  - `dataguard_broker.yml`: Enables and configures DG Broker.
- **Requirements**: Oracle 19c zip, SSH keys, firewall ports open (1521/tcp, 5500/tcp), Ansible vault for passwords.
- **Tested On**: Oracle Linux VMs with bridge adapter, development/security/performance tools.

## Setup and Usage
1. Prep software: Download Oracle 19c, place in /tmp via scp or WinSCP.
2. Configure SSH/firewall (see docs/environmental-setup.md).
3. Clone repo, update inventory.
4. Encrypt secrets: `ansible-vault encrypt secrets.yml`.
5. Run main playbook: `ansible-playbook -i inventory oracle_dg_setup.yml --ask-vault-pass`.
6. Run broker: `ansible-playbook -i inventory dataguard_broker.yml --ask-vault-pass`.

See docs/environmental-setup.md for full prep.


