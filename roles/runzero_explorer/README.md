<!-- DOCSIBLE START -->
# runzero_explorer

## Description

Install the runZero explorer

## Requirements

- Ansible >= 2.14

## Role Variables

### Default Variables (main.yml)

| Variable | Type | Default | Description |
| -------- | ---- | ------- | ----------- |
| `runzero_explorer_log_debug` | str | <code>false</code> | No description |
| `runzero_explorer_systemd_enabled` | str | <code>false</code> | No description |
| `runzero_explorer_version_id` | str | <code>1a430dd4</code> | No description |

### Role Variables (main.yml)

| Variable | Type | Value | Description |
| -------- | ---- | ----- | ----------- |
| `runzero_explorer_chromium_package` | str | `{{ 'chromium-browser' if ansible_distribution == 'Ubuntu' and ansible_distribution_version is version('20.04', '>=') else 'chromium' }}` | No description |
| `runzero_explorer_common_install_packages` | list | `[]` | No description |
| `runzero_explorer_debian_packages` | list | `[]` | No description |
| `runzero_explorer_debian_packages.0` | str | `{{ runzero_explorer_chromium_package }}` | No description |
| `runzero_explorer_debian_packages.1` | str | `curl` | No description |
| `runzero_explorer_debian_packages.2` | str | `wireless-tools` | No description |
| `runzero_explorer_el_packages` | list | `[]` | No description |
| `runzero_explorer_el_packages.0` | str | `{{ runzero_explorer_chromium_package }}` | No description |
| `runzero_explorer_el_packages.1` | str | `iw` | No description |
| `runzero_explorer_nix_path` | str | `/opt/runzero/bin/runzero-explorer.bin` | No description |
| `runzero_explorer_windows_path` | str | `C:\runzero-explorer.exe` | No description |
| `runzero_explorer_url` | str | `https://console.runzero.com/download/explorer` | No description |

## Tasks

### main.yml


- **Set runzero_explorer_path** (ansible.builtin.set_fact)
- **Set architecture mapping for runzero-explorer** (ansible.builtin.set_fact)
- **Determine runzero-explorer binary architecture** (ansible.builtin.set_fact) - Conditional
- **Check if RUNZERO_DOWNLOAD_TOKEN is set** (ansible.builtin.fail) - Conditional
- **Set the unique token** (ansible.builtin.set_fact)
- **Create the directory for the runzero-explorer binary** (ansible.builtin.file)
- **Include tasks for Unix-like systems** (ansible.builtin.include_tasks) - Conditional
- **Include systemd tasks** (ansible.builtin.include_tasks) - Conditional
- **Include tasks for Windows** (ansible.builtin.include_tasks) - Conditional

### systemd.yml


- **Create runZero Explorer systemd service file** (ansible.builtin.copy)
- **Enable and start runZero Explorer service** (ansible.builtin.systemd)

### unix.yml


- **Set runzero-explorer download URL for Unix-like systems** (ansible.builtin.set_fact) - Conditional
- **Set runzero-explorer download URL for Darwin systems** (ansible.builtin.set_fact) - Conditional
- **Set RUNZERO_AGENT_LOG_DEBUG environment variable** (ansible.builtin.lineinfile)
- **Generate a unique RUNZERO_AGENT_HOST_ID** (ansible.builtin.set_fact) - Conditional
- **Set RUNZERO_AGENT_HOST_ID environment variable** (ansible.builtin.lineinfile)
- **Install required packages for runZero Explorer** (ansible.builtin.include_role)
- **Create runZero Explorer directory** (ansible.builtin.file)
- **Check if runzero-explorer already exists** (ansible.builtin.stat)
- **Download runzero-explorer** (ansible.builtin.get_url) - Conditional
- **Find runzero-agent files** (ansible.builtin.find)
- **Get hash of existing runzero-explorer file** (ansible.builtin.stat) - Conditional
- **Rename the most recent runzero-agent file to the default destination** (ansible.builtin.command) - Conditional
- **Execute runzero-explorer** (ansible.builtin.command) - Conditional

### windows.yml


- **Set runzero-explorer download URL for Windows** (ansible.builtin.set_fact) - Conditional
- **Check if runzero-explorer already exists** (ansible.windows.win_stat)
- **Download runzero-explorer** (ansible.windows.win_get_url) - Conditional
- **Find runzero-agent files (if applicable)** (ansible.windows.win_find)
- **Get hash of existing runzero-explorer file (if applicable)** (ansible.windows.win_stat) - Conditional
- **Rename the most recent runzero-agent file to the default destination (if applicable)** (ansible.windows.win_command) - Conditional
- **Execute runzero-explorer** (ansible.windows.win_command) - Conditional

## Example Playbook

```yaml
- hosts: servers
  roles:
    - runzero_explorer
```

## Author Information

- **Author**: Jayson Grace
- **Company**: l50
- **License**: MIT

## Platforms


- Ubuntu: all
- Debian: all
- Kali: all
- EL: all
- Windows: all
<!-- DOCSIBLE END -->
