# Environmental Setup for Oracle Data Guard Ansible Deployment

## VM/Host Requirements
- OS: Oracle Linux 7/8.
- Networking: Bridge adapter for primary-standby comms.
- GUI Add-Ons (yum groupinstall):
  - "Development Tools": gcc, make for Oracle builds.
  - "Security Tools": Firewall management.
  - "Performance Tools": Tuning utilities.
  - "System Administration Tools": Network/firewall config.
  - "Compatibility Libraries": libaio, compat-libcap1 for Oracle 19c.

## Software Preparation
1. Download Oracle 19c (LINUX.X64_193000_db_home.zip) from Oracle site.
2. Place on targets:
   - Via scp: `scp LINUX.X64_193000_db_home.zip oracle@prod-server:/tmp/` (same for standby).
   - Alternative: Use WinSCP for manual transfer if scp is slow.

## SSH Configuration
- Generate key: `ssh-keygen -t rsa -b 4096 -C "ansible@ansible-server"`.
- Copy: `ssh-copy-id oracle@prod-server` (same for standby).
- Test: `ssh oracle@prod-server "hostname; date"` (same for standby).

## Firewall Configuration
On all servers:
# On both servers
sudo firewall-cmd --permanent --add-port=1521/tcp
sudo firewall-cmd --permanent --add-port=5500/tcp
sudo firewall-cmd --reload


## /etc/hosts
Add for resolution:
127.0.0.1   localhost localhost.localdomain
192.168.1.99 ansible-server.localdomain ansible-server
192.168.1.100 prod-server.localdomain prod-server
192.168.1.101 standby-server.localdomain standby-server


## Ansible Setup
- ansible.cfg/inventory as provided.
[primary]
prod-server ansible_host=192.168.1.100 ansible_user=oracle db_sid=PROD

[standby]
standby-server ansible_host=192.168.1.101 ansible_user=oracle db_sid=PROD

[all:vars]
ansible_connection=ssh
ansible_ssh_common_args='-o StrictHostKeyChecking=no'


- Vault: `ansible-vault create secrets.yml` with `sys_password: Oracle123`.
