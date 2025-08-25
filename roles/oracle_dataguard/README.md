# Role: oracle_dataguard

This role configures Oracle Data Guard for a physical standby, including PFILE/SPFILE setup, network config (listener/tnsnames), password file copy, RMAN duplication, DG parameters (log_archive_dest, FAL, standby logs), MRP enablement, and basic replication testing.

## Tasks Overview
- Standby dir creation.
- Env profile setup.
- Network config templates.
- PFILE mod and SPFILE creation.
- Primary/standby param config (FORCE LOGGING, ASYNC transport).
- RMAN active duplicate.
- Standby mount and redo apply.
- Test table insert/verification.

## Variables
- oracle_home, db_sid, sys_password (from vault).
- Templates: listener.ora.j2, tnsnames.ora.j2 (dynamic hosts).
- Handlers: Restart listener on changes.

## Usage
Run on all hosts after installation. Delegate tasks use groups['primary']/['standby'].

## Dependencies
- oracle_install role completed on primary.
- TNS connectivity between hosts.
- Integrates with dataguard_broker.yml for broker setup post-DG config.
