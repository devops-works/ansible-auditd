# ansible-auditd2json

Installs auditd2json (https://gitlab.com/devopsworks/tools/auditd2json)

This role does not check if auditd2json is already installed and overrides
existing binary (no way to check version in auditd2json yet).

## Variables

- `auditd2json_force_install`: forces installation of auditd2json even if it is
  already installed
  