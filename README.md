# Ansible Collection: Bulwark

[![License](https://img.shields.io/github/license/l50/ansible-collection-bulwark?label=License&style=flat&color=blue&logo=github)](https://github.com/l50/ansible-collection-bulwark/blob/main/LICENSE)
[![Pre-Commit](https://github.com/l50/ansible-collection-bulwark/actions/workflows/pre-commit.yaml/badge.svg)](https://github.com/l50/ansible-collection-bulwark/actions/workflows/pre-commit.yaml)
[![Molecule Test](https://github.com/l50/ansible-collection-bulwark/actions/workflows/molecule.yaml/badge.svg)](https://github.com/l50/ansible-collection-bulwark/actions/workflows/molecule.yaml)
[![Renovate](https://github.com/l50/ansible-collection-bulwark/actions/workflows/renovate.yaml/badge.svg)](https://github.com/l50/ansible-collection-bulwark/actions/workflows/renovate.yaml)

This Ansible collection provides setup and configuration for defensive security
tools, covering utilities and applications for threat detection, incident
response, and system hardening.

## Requirements

- Ansible 2.15 or higher

## Installation

Install the latest version of the Bulwark collection:

```bash
ansible-galaxy collection install git+https://github.com/l50/ansible-collection-bulwark.git,main
```

## Roles

### runZero Explorer

Installs and configures [runZero Explorer](https://console.runzero.com/deploy/download/explorers).

## Usage

Include the roles from this collection in your playbook. Here's an example:

```yaml
---
- name: Provision container
  hosts: localhost
  roles:
    - l50.bulwark.runzero_explorer
    ...
```

## License

This collection is licensed under the MIT License - see the [LICENSE](LICENSE)
file for details.

## Support

- Repository: [l50/ansible-collection-bulwark](https://github.com/l50/ansible-collection-bulwark)
- Issue Tracker: [GitHub Issues](https://github.com/l50/ansible-collection-bulwark/issues)

## Authors

- Jayson Grace ([techvomit.net](https://techvomit.net))
