# Ansible Playbook: RunZero Explorer

This playbook deploys the RunZero Explorer agent on Ubuntu and Kali Linux
hosts. RunZero Explorer is a network discovery and asset inventory tool that
provides comprehensive visibility into your network infrastructure.

## Table of Contents

- [Base Requirements](#base-requirements)
- [Quick Start](#quick-start)
- [Usage](#usage)
  - [Basic Playbook Execution](#basic-playbook-execution)
  - [Local Machine Setup](#local-machine-setup)
  - [Targeting Specific Hosts](#targeting-specific-hosts)
- [Testing](#testing)
- [Configuration](#configuration)
- [Example Inventory](#example-inventory)
- [Security Considerations](#security-considerations)
- [Troubleshooting](#troubleshooting)

---

## Base Requirements

- **Ansible** 2.14 or higher
- **Python** 3.8 or higher
- **Operating Systems**: Ubuntu 24.04 or Kali Linux
- **Memory**: Minimum 1GB RAM recommended
- **Network**: Outbound HTTPS connectivity to RunZero cloud services

### Python Package Installation

Install required Python packages:

```bash
python3 -m pip install --upgrade \
  ansible-core \
  molecule \
  molecule-docker \
  "molecule-plugins[docker]"
```

### Ansible Collections and Roles

Install required collections and roles:

```bash
ansible-galaxy install -r requirements.yml
```

---

## Quick Start

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

1. Install dependencies:

   ```bash
   ansible-galaxy install -r requirements.yml
   ```

1. Configure your RunZero credentials (see [Configuration](#configuration))

1. Run the playbook:

   ```bash
   ansible-playbook runzero_explorer.yml -i inventory
   ```

---

## Usage

### Basic Playbook Execution

Run the playbook against all hosts in your inventory:

```bash
ansible-playbook runzero_explorer.yml -i inventory
```

### Local Machine Setup

To install RunZero Explorer on your local machine:

```bash
ansible-playbook runzero_explorer.yml -i molecule/default/inventory
```

### Targeting Specific Hosts

Run against specific host groups:

```bash
ansible-playbook runzero_explorer.yml -i inventory --limit "scanners"
```

### With Extra Variables

Pass RunZero configuration at runtime:

```bash
ansible-playbook runzero_explorer.yml -i inventory \
  -e runzero_organization_id=YOUR_ORG_ID \
  -e runzero_site_id=YOUR_SITE_ID \
  -e runzero_token=YOUR_TOKEN
```

---

## Testing

This playbook includes Molecule tests for both Ubuntu 24.04 and Kali Linux environments.

### Running Tests

```bash
# Run the full test sequence
molecule test

# Or run individual steps
molecule create      # Create test instances
molecule converge    # Deploy the playbook
molecule verify      # Run verification tests
molecule destroy     # Clean up test instances

# Test with custom playbook
MOLECULE_PLAYBOOK=custom.yml molecule converge
```

### Test Platforms

The molecule configuration includes:

- **Ubuntu 24.04**: Using `geerlingguy/docker-ubuntu2404-ansible:latest`
- **Kali Linux**: Using `cisagov/docker-kali-ansible:latest`

Both platforms run with:

- Privileged mode enabled
- CGroup filesystem mounted
- Host cgroupns mode

---

## Configuration

The playbook uses the `l50.bulwark.runzero_explorer` role. Configuration
options should be set according to your RunZero deployment.

### Required Variables

These variables must be configured for the RunZero Explorer to function:

```yaml
# RunZero Organization Settings
runzero_organization_id: "YOUR_ORGANIZATION_ID"
runzero_site_id: "YOUR_SITE_ID"
runzero_token: "YOUR_EXPLORER_TOKEN"
```

### Optional Variables

Additional configuration options may be available through the role. Consult the
`l50.bulwark.runzero_explorer` role documentation for a complete list.

### Setting Variables

Variables can be set in multiple ways:

1. **In your inventory file**:

   ```ini
   [scanners:vars]
   runzero_organization_id=org_123456
   runzero_site_id=site_789012
   ```

1. **In a group_vars file** (`group_vars/all.yml`):

   ```yaml
   runzero_organization_id: "org_123456"
   runzero_site_id: "site_789012"
   runzero_token: !vault |
     $ANSIBLE_VAULT;1.1;AES256
     66383439383437...
   ```

---

## Example Inventory

### Local Installation

Using the provided inventory at `molecule/default/inventory`:

```ini
[local]
localhost ansible_connection=local
```

### Remote Hosts

Create an inventory file for your RunZero Explorer hosts:

```ini
[scanners]
scanner1 ansible_host=192.168.1.100
scanner2 ansible_host=192.168.1.101

[scanners:vars]
ansible_user=ubuntu
ansible_become=true
ansible_ssh_private_key_file=~/.ssh/runzero_key
```

### Multi-Site Deployment

```ini
[site_a]
scanner-a1 ansible_host=10.1.1.10
scanner-a2 ansible_host=10.1.1.11

[site_b]
scanner-b1 ansible_host=10.2.1.10
scanner-b2 ansible_host=10.2.1.11

[site_a:vars]
runzero_site_id=site_aaaaaa

[site_b:vars]
runzero_site_id=site_bbbbbb

[all:vars]
runzero_organization_id=org_123456
ansible_user=ubuntu
ansible_become=true
```

---

## Security Considerations

### Best Practices

1. **Credential Management**:

   - Never commit RunZero tokens to version control
   - Use Ansible Vault to encrypt sensitive variables
   - Rotate tokens regularly

1. **Network Security**:

   - RunZero Explorer requires outbound HTTPS (443) to RunZero cloud
   - No inbound ports required
   - Consider network segmentation for scanner placement

1. **Access Control**:
   - Limit access to hosts running RunZero Explorer
   - Use principle of least privilege for the service account
   - Monitor explorer activity through RunZero console

### Ansible Vault Usage

Encrypt sensitive variables:

```bash
# Create encrypted variables file
ansible-vault create group_vars/all/vault.yml

# Edit encrypted file
ansible-vault edit group_vars/all/vault.yml

# Run playbook with vault
ansible-playbook runzero_explorer.yml -i inventory --ask-vault-pass
```

---

## Troubleshooting

### Common Issues

1. **Explorer Not Starting**

   ```bash
   # Check service status
   sudo systemctl status runzero-explorer

   # View logs
   sudo journalctl -u runzero-explorer -f
   ```

1. **Authentication Failures**

   - Verify organization ID and site ID are correct
   - Ensure token has not expired
   - Check network connectivity to RunZero cloud

1. **Network Discovery Issues**
   - Verify explorer has necessary network access
   - Check local firewall rules
   - Ensure no conflicting network scanners

### Debug Mode

Run the playbook with increased verbosity:

```bash
ansible-playbook runzero_explorer.yml -i inventory -vvv
```

### Verification

After deployment, verify the explorer is running:

```bash
# Check service
sudo systemctl is-active runzero-explorer

# Verify in RunZero Console
# Navigate to Inventory → Explorers to see your deployed explorers
```
