==============================================
Bulwark Ansible Collection 1.0.0 Release Notes
==============================================

.. contents:: Topics

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
