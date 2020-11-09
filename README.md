# Ansible role for suricata

## Requirements
* tested with Debian Stretch

## Defaults

```
suricata_default_tpl: "default_suricata.j2"
suricata_interface: "eth0"
suricata_tpl: "suricata.yaml.j2"
```

## Role Variables

| Variable name                  | Type         | Default                                   | Description                                                     |
| ------------------------------ | ------------ | ----------------------------------------- | --------------------------------------------------------------- |
| suricata_tpl                   | path         | suricata.yaml.j2                          | The suricata YAMl config template to be used                    |
| suricata_default_tpl           |              | default_suricata.j2                       | The suricata default file template to be used                   |
| suricata_interface             | iface        | eth0                                      | The interface suricata should monitor                           |
| suricata_pcap_log              | bool         | true                                      | If suricata should save the packets in the pcap.log file or not |
| suricata_home_nets             | list[cidr]   | [192.168.0.0/16,10.0.0.0/8,172.16.0.0/12] | List of home nets for this host                                 |
| suricata_external_net          | string       | !$HOME_NET                                | The external net address group                                  |
| suricata_address_groups        | dict[string] | \*1                                       | Dictionary containing address group definitions                 |
| suricata_port_groups           | dict[string] | \*2                                       | Dictionary containing port group definitions                    |
| suricata_rule_path             | path         | /etc/suricata/rules                       | The path to the rules directory                                 |
| suricata_rule_files            | list[string] |                                           | The rule files suricata should use                              |
| suricata_extra_rule_files      | list[path]   | []                                        | List of additional rule files to install on the host            |
| suricata_classification_file   | path         | /etc/suricata/classification.config       | The path to the classification file                             |
| suricata_reference_config_file | path         | /etc/suricata/reference.config            | The path to the reference config file                           |
| suricata_threshold_file        | path         |                                           | The path to the threshold config file                           |
| suricata_log_dir               | path         | /var/log/suricata/                        | The default suricata log directory                              |
|                                |              |                                           |                                                                 |
|                                |              |                                           |                                                                 |
|                                |              |                                           |                                                                 |
|                                |              |                                           |                                                                 |

### \*1
```
suricata_address_groups:
    HTTP_SERVERS: "$HOME_NET"
    SMTP_SERVERS: "$HOME_NET"
    SQL_SERVERS: "$HOME_NET"
    DNS_SERVERS: "$HOME_NET"
    TELNET_SERVERS: "$HOME_NET"
    AIM_SERVERS: "$EXTERNAL_NET"
    DNP3_SERVER: "$HOME_NET"
    DNP3_CLIENT: "$HOME_NET"
    MODBUS_CLIENT: "$HOME_NET"
    MODBUS_SERVER: "$HOME_NET"
    ENIP_CLIENT: "$HOME_NET"
    ENIP_SERVER: "$HOME_NET"
```

### \*2
```
suricata_port_groups:
    HTTP_PORTS: "80"
    SHELLCODE_PORTS: "!80"
    ORACLE_PORTS: 1521
    SSH_PORTS: 22
    DNP3_PORTS: 20000
    MODBUS_PORTS: 502
```

## Use
```
- hosts: localhost
  roles:
        - suricata
  vars:
          suricata_interface: "enp0s3"

```

