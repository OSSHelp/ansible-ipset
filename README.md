# ipset

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/ipset/status.svg)](https://drone.osshelp.ru/ansible/ipset)

The role installs and configure ipset

## Usage (examples)

### Minimal

```yaml
    - role: ipset
```

### Cloudflare + custom lists

```yaml
    - role: ipset
      lists:
        - {name: cf-v4, family: inet}
        - {name: cf-v6, family: inet6}
        - {name: client-ssh, family: inet, uri: http://projectname.ossdata.ru/ipset136/client-ssh}
```

### Custom ipset lists with list of IP

```yaml
- role: ipset
  update_lists: false
  lists:
    - name: custom-v4
      family: inet
      ips:
        - 123.123.123.123
        - 234.234.234.234
    - name: custom-v6
      family: inet6
      ips:
        - 2001:19f0:210:125d::436
        - 2607:fcd0:bb70:1e00::4020
```

## Available parameters

### Main

| Param | Default | Description |
| -------- | -------- | -------- |
| `ipset_setup` | `full` | Setup mode. See [OSSHelp KB article](https://oss.help/kb4895) |
| `ipset_default_lists` | See next header. | Default ipset lists |
| `lists` | `[]` | Custom ipset lists |

### List parameters

By default the role installs 4 ipset lists:

```yaml
ipset_default_lists:
  - {name: oss-v4, family: inet}
  - {name: oss-v6, family: inet6}
  - {name: oss-probe-v4, family: inet}
  - {name: oss-probe-v6, family: inet6}
```

Additonal lists can be enabled using these parameters:

| Param | Default | Description |
| -------- | -------- | -------- |
| `name` | - | name of an ipset list, any name, e.g. `client-ssh` |
| `family` | - | family of an ipset list, `inet` or `inet6` |
| `uri` | - | url which contains a list of IPs for a specific ipset list |
| `ips` | - | list of IP adresses for list |

## Useful links

- [custom.refresh-ipset description](https://oss.help/kb8)
- [Old ipset setup guide](https://oss.help/kb482)
- [How to use ipset with iptables](https://oss.help/kb485)

## TODO

- improve check mode support. Some task disabled for check mode
- delete update_lists param

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
