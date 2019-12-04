# Ansible role `sysctl`

An Ansible role for centralizing kernel parameters through `sysctl`.
Specifically, the responsibilities of this role are to:

- Install a clean and consistent sysctl base configuration
- Set OpenIO kernel parameters
- Allow legacy or customer kernel parameters

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_sysctl_namespace` | "OPENIO" | The namespace |
| `openio_sysctl_kernel_entries` | `{}` | A dictionnary with OpenIO parameters and values. |
| `openio_sysctl_legacy_kernel_files` | `{}` | A list of dictionnaries with legacy/Customer filename, parameters and values. |

## Dependencies

No dependencies.

## Example Playbook

```yaml
- hosts: all
  gather_facts: true
  become: true
    NS: OPENIO
  roles:
    - role: sysctl
      openio_sysctl_namespace: "{{ NS }}"
      openio_sysctl_kernel_entries:
        net.ipv4.tcp_fastopen: 1
      openio_sysctl_legacy_kernel_files:
        - filename: "99-security.conf"
          entries:
            kernel.sysrq: 0
            kernel.core_uses_pid: 1
        - filename: "98-network.conf"
          entries:
            net.ipv4.tcp_syncookies: 1
            net.ipv4.tcp_synack_retries: 5
```

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome.
The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork.
Github can then easily create a PR based on that branch.

## License

GNU AFFERO GENERAL PUBLIC LICENSE, Version 3

## Contributors

- [Cedric DELGEHIER](https://github.com/cdelgehier) (maintainer)
- [Jérôme LOYET](https://github.com/fatpat) (maintainer)
