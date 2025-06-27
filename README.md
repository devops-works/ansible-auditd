# ansible-auditd

Installs auditd

## Variables

- `auditd_local_rulesets`: install a local (i.e. include in role) ruleset; see
  `*.rules.j2`files in the [templates](./templates/) directory
- `auditd_source_rulesets`: install rulesets provided in auditd source; see
  https://github.com/linux-audit/audit-userspace/tree/master/rules for a list
- `auditd_custom_rules`: custom rules to set in /etc/auditd/rules.d/98-custom.conf

Note that `/etc/auditd/rules.d/98-custom.conf` is always generated. If you
change this file it will be overwritten by this role.

## Testing

You can test this role using molecule and the docker driver
(e.g. `molecule test`)

## Examples

```yaml
---
- name: Run
  hosts: all
  gather_facts: yes
  roles:
    - role: ansible-auditd
      auditd_local_rulesets: ["38-anssi","39-neo23x0"]
      auditd_source_rulesets: ["30-stig","41-containers"]
      auditd_custom_rules:
      - "-a exit,always -F arch=b64 -S unlink -S rmdir -S rename -k fschange"
      - "-a exit,always -F arch=b64 -S creat -S open -S openat -F exit=-EACCES -k fschange"
      - "-a exit,always -F arch=b64 -S truncate -S ftruncate -F exit=-EACCES -k fschange"
```