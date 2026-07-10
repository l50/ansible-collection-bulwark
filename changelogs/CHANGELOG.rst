==============================================
Bulwark Ansible Collection 1.1.0 Release Notes
==============================================

.. contents:: Topics

v1.1.0
======

Release Summary
---------------

Feature release introducing five new Ansible roles for cloud infrastructure management, Windows host instrumentation, and security monitoring, plus reliability and security improvements to the runzero_explorer role.

Added
-----

- aws_cloudwatch_agent - New Ansible role for deploying and configuring AWS CloudWatch Agent across supported platforms (#524).
- aws_cloudwatch_agent, aws_ssm_agent - Added Molecule test suites for integration testing (#529).
- aws_ssm_agent - New Ansible role for cross-platform AWS Systems Manager Agent management (#525).
- dc_audit_sacl - New Ansible role for configuring Domain Controller audit SACL policies to support attack detection (#523).
- grafana_alloy - New Ansible role for Grafana Alloy deployment targeting Windows event log collection and forwarding (#526).
- runzero_explorer - Added resilient download configuration with retry logic for improved reliability in network-constrained environments (#509).
- sysmon - New Ansible role for Windows host instrumentation using Sysinternals Sysmon (#522).

Changed
-------

- Updated Ansible collection dependencies (amazon.aws 11.4.0, ansible.windows 3.6.1, community.general 13.x) and ansible-core to 2.21.1.
- Updated Python, Go, and Task tooling versions across CI workflows.

Fixed
-----

- README - Fixed roles table markers so the pre-commit hook passes validation (#497).

v1.0.1
======

Release Summary
---------------

Enhanced CI/CD workflows, improved documentation generation, updated dependencies, and refined the runzero_explorer role with better testing and documentation

Added
-----

- Added `docsible` integration for automatic Ansible role documentation generation with custom templates
- Added architecture diagram generation using Mermaid for visual collection structure representation
- Added comprehensive release documentation in `docs/releases.md`
- Added markdownlint-cli for improved markdown linting
- Added merge group support in CI workflows for better PR queue management
- Added support for manual workflow dispatch with role/playbook selection in molecule workflow
- Added template sync workflow for keeping infrastructure files up-to-date with the ansible collection template

Changed
-------

- Enhanced Renovate configuration with custom git author, dashboard labels, and simplified package rules
- Enhanced runzero_explorer role with improved variable naming and documentation
- Fixed molecule test configurations for better Docker container management
- Fixed pre-commit hook configurations for proper file handling
- Fixed variable naming consistency in runzero_explorer role (runzero_agent_* to runzero_explorer_agent_*)
- Improved molecule workflow with better concurrency control and input validation
- Refactored pre-commit configuration to use markdownlint-cli instead of Ruby-based mdl
- Updated Ansible collection dependencies (amazon.aws 10.1.1, ansible.windows 3.2.0, community.docker 4.7.0, community.general 11.2.1)
- Updated GitHub Actions to latest versions (create-github-app-token v2.1.1, checkout v5.0.0, setup-python v5.6.0, cache v4.2.4)
- Updated Python dependencies to latest stable versions (ansible-core 2.19.1, molecule 25.7.0, pre-commit 4.3.0)

Removed
-------

- Removed RedHat platform from runzero_explorer molecule tests
- Removed Ruby-based markdown linter (mdl) in favor of markdownlint-cli
- Removed custom regex managers from Renovate configuration

v1.0.0
======

Release Summary
---------------

Introduced the `runzero_explorer` role, automated release playbook, and improved GitHub Actions workflows for streamlined testing and deployment

Added
-----

- Added a new GitHub Actions workflow `molecule.yaml` for running Molecule tests on pull requests and pushes.
- Added role `runzero_explorer` with tasks for installing and managing the runZero Explorer across various platforms.
- Automated Release Playbook - Introduced `galaxy-deploy.yml`, an automated release playbook for publishing the collection to Ansible Galaxy.
- Renovate Bot Configuration - Updated Renovate Bot configurations to reflect the new repository structure and naming.
