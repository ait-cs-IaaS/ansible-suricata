# Ansible role for suricata

# Requirements
* tested with Debian Stretch

# Defaults

```
suricata_default_tpl: "default_suricata.j2"
suricata_interface: "eth0"
suricata_tpl: "suricata.yaml.j2"
```

# Use
```
- hosts: localhost
  roles:
        - suricata
  vars:
          suricata_interface: "enp0s3"

```
