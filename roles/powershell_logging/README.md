<!-- DOCSIBLE START -->
# powershell_logging

## Description

Enable PowerShell script block and module logging for attack detection

## Requirements

- Ansible >= 2.14

## Role Variables

### Default Variables (main.yml)

| Variable | Type | Default | Description |
| -------- | ---- | ------- | ----------- |
| `powershell_logging_enable_script_block` | bool | <code>True</code> | No description |
| `powershell_logging_enable_script_block_invocation` | bool | <code>False</code> | No description |
| `powershell_logging_enable_module_logging` | bool | <code>True</code> | No description |
| `powershell_logging_module_names` | list | <code>&#91;&#93;</code> | No description |
| `powershell_logging_module_names.0` | str | <code>*</code> | No description |
| `powershell_logging_enable_transcription` | bool | <code>False</code> | No description |
| `powershell_logging_transcript_output_directory` | str | <code>C:\ProgramData\PSTranscripts</code> | No description |
| `powershell_logging_transcription_invocation_header` | bool | <code>True</code> | No description |
| `powershell_logging_operational_max_size_mb` | int | <code>256</code> | No description |
| `powershell_logging_policy_key` | str | <code>HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell</code> | No description |
| `powershell_logging_operational_channel` | str | <code>Microsoft-Windows-PowerShell/Operational</code> | No description |

## Tasks

### main.yml


- **Configure script block logging (event 4104)** (ansible.windows.win_regedit)
- **Configure script block invocation logging (events 4105/4106)** (ansible.windows.win_regedit)
- **Configure module logging (event 4103)** (ansible.windows.win_regedit)
- **Register modules for pipeline logging** (ansible.windows.win_regedit) - Conditional
- **Configure transcription** (block) - Conditional
- **Ensure transcript output directory exists** (ansible.windows.win_file)
- **Enable transcription** (ansible.windows.win_regedit)
- **Set transcript output directory** (ansible.windows.win_regedit)
- **Configure transcript invocation header** (ansible.windows.win_regedit)
- **Size the PowerShell Operational channel** (block) - Conditional
- **Read current Operational channel size** (ansible.windows.win_shell)
- **Set Operational channel size** (ansible.windows.win_shell) - Conditional
- **Verify PowerShell logging policy** (ansible.windows.win_shell)
- **Display verification result** (ansible.builtin.debug)

## Example Playbook

```yaml
- hosts: servers
  roles:
    - powershell_logging
```

## Author Information

- **Author**: Jayson Grace
- **Company**: l50
- **License**: MIT

## Platforms


- Windows: 2019, 2022
<!-- DOCSIBLE END -->
