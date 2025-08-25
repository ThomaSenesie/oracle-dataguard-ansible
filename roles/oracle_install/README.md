# Role: oracle_install

This role installs Oracle 19c software, creates necessary directories, extracts binaries, runs silent installer, creates the primary database using DBCA, and sets initial parameters (e.g., ARCHIVELOG, FRA).

## Tasks Overview
- Directory creation (/u01, /u02 paths).
- Binary extraction and installation via runInstaller with response file.
- DB creation on primary only.
- Parameter settings (processes, ARCHIVELOG).

## Variables
- From vars/main.yml: oracle_home, ora_inventory, db_name, etc.
- Templates: install.rsp.j2, dbca.rsp.j2 (customize passwords, memory).

## Usage
Include in playbook for primary hosts. Ensure Oracle zip is in /tmp.

## Dependencies
- Ansible sudo access.
- Pre-installed prereqs (libaio, etc.).
- Assumes Oracle zip in /tmp; see docs for prep.
