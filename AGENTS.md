# Project Overview

This repository contains the `community.beszel` Ansible Collection. It follows the standard Ansible Collection structure. This file is intended for use by AI agents to execute tasks within this project.

## Contributor Workflow

Before making changes, read and follow [`CONTRIBUTING.md`](CONTRIBUTING.md). It is the source of truth for setting up the development environment, managing dependencies, running tests and lint checks, and creating changelog fragments. Do not duplicate those instructions in this file.

## Coding Guidelines

- Ansible plugins and modules should be formatted using `ruff`.
- Format Ansible plugins and modules from the project root using the command: `uv run ruff format plugins/`.
- Ansible plugins and modules should use the standard snake_case variable convention.
- Ansible plugins and modules should pass sanity, unit and integration tests.
- Validate changes using the relevant checks documented in [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Architecture

- The repository follows the standard Ansible Collection structure.
- Ansible roles are located in the `roles` directory.
- Ansible plugins and modules are located in the `plugins` directory. Modules specifically are located in `plugins/modules`.
- A Python function which is used by multiple modules should be implemented in the `plugins/module_utils` directory. This ensures code conforms to DRY (Don't repeat yourself) principle.
- Ansible [Molecule](https://docs.ansible.com/projects/molecule/) scenarios are located in the `extensions/molecule` directory.
- Each Ansible role should contain at least one Molecule scenario.
- The `version` in the [`pyproject.toml`](pyproject.toml) file should match the `version` in the [`galaxy.yml`](galaxy.yml) file.
