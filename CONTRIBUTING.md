# Contributing

## Getting Started

The `community.beszel` Ansible collection uses [uv](https://docs.astral.sh/uv/) and [Ansible Development Environment (ADE)](https://github.com/ansible/ansible-dev-environment) for collection development. The recommended method for [installing](https://github.com/ansible/ansible-dev-environment?tab=readme-ov-file#installation) ADE is using [`uv`](https://docs.astral.sh/uv/):

```bash
uv tool install ansible-dev-environment
```

Once ADE is installed, follow the steps below for contributing to `community.beszel`:

1. [Fork](https://github.com/ansible-collections/community.beszel/fork) the `community.beszel` collection.

2. Clone your fork of the `community.beszel` collection:

    ```bash
    git clone https://github.com/YOUR_USERNAME/community.beszel.git
    cd community.beszel
    ```

3. Create your feature branch:

    ```bash
    git checkout -b feature/my-new-feature
    ```

4. Initialize the development environment using `uv` and ADE:

    ```bash
    # Install development dependencies
    uv sync --dev
    # Install pre-commit hooks
    uv run prek install
    # Install collection dependencies
    uv pip install -r meta/ee-requirements.txt
    # Install the collection into the Python virtual environment
    ade install --editable --no-seed .
    ```

You are now ready to begin developing the collection. Please familiarize yourself with the [Ansible community guide](https://docs.ansible.com/ansible/devel/community/index.html).

When you are ready to merge your changes from your fork, create a pull request in this repository.

## Python Development Dependencies

Python dependencies used for developing the collection are defined in the [`pyproject.toml`](pyproject.toml) `dev` dependency group.

Add a new Python development dependency:

```bash
uv add <package> --dev
```

## Python Collection Dependencies

Python collection dependencies are defined in [`meta/ee-requirements.txt`](meta/ee-requirements.txt). Dependencies declared in this file are required by the collection at runtime.

## Running pre-commit Hooks

The pre-commit hooks are defined in [.pre-commit-config.yaml](.pre-commit-config.yaml) file.

Run all pre-commit hooks using [`prek`](https://prek.j178.dev/) from the project root:

```bash
uv run prek run --all-files
```

## Collection Tests

The `community.beszel` Ansible collection uses [`tox-ansible`](https://github.com/ansible/tox-ansible) to run its unit, integration and sanity test environments across the supported Python and `ansible-core` versions.

View the `tox-ansible` test environments:

```bash
uv run tox --ansible -l
```

Run a specific test environment:

```bash
uv run tox --ansible -e <environment>
```

Run the complete test matrix:

```bash
uv run tox --ansible
```

### Unit Tests

Unit tests are located in the [`tests/unit`](tests/unit/) directory.

The `tox-ansible` unit test environment names are prefixed with `unit-*`.

Unit test collection dependencies are defined in [`tests/unit/requirements.yml`](tests/unit/requirements.yml).

Run all the unit test environments:

```bash
uv run tox --ansible -f unit
```

Run a specific unit test environment for Python 3.11 and `ansible-core` 2.19:

```bash
uv run tox --ansible -e unit-py3.11-2.19
```

### Integration Tests

> [!IMPORTANT]
> You **must** have a Docker compatible container runtime to run the integration tests locally.

Integration tests are located in the [`extensions/molecule`](extensions/molecule/) directory. Each subdirectory is a [Molecule](https://ansible.readthedocs.io/projects/molecule/index.html) scenario.

The `tox-ansible` integration test environment names are prefixed with `integration-*`.

Integration test collection dependencies are defined in [`tests/integration/requirements.yml`](tests/integration/requirements.yml).

Integration test Python dependencies are defined in [`tests/integration/requirements.txt`](tests/integration/requirements.txt).

Integration tests are triggered using the [`pytest-ansible` Molecule fixture](https://docs.ansible.com/projects/pytest-ansible/getting_started/#molecule-scenario-integration) located in [`tests/integration/test_integration.py`](tests/integration/test_integration.py).

<!-- Mermaid Diagram showing the above here -->

Run all the integration test environments:

```bash
uv run tox --ansible -f integration
```

Run a specific integration test environment for Python 3.11 and `ansible-core` 2.19:

```bash
uv run tox --ansible -e integration-py3.11-2.19
```

### Sanity Tests

Run the sanity test environments:

```bash
uv run tox --ansible -f sanity
```

Run a specific sanity test environment for Python 3.11 and `ansible-core` 2.19:

```bash
uv run tox --ansible -e sanity-py3.11-2.19
```

### Static Analysis - Ansible lint

The `community.beszel` Ansible collection uses [`ansible-lint`](http://ansible.readthedocs.io/projects/lint/) to lint Ansible roles and playbooks located in the `roles` and `playbooks` directories respectively.

Run `ansible-lint`:

```bash
uv run ansible-lint -v
```

The [.ansible-lint](.ansible-lint) configuration file is used to configure the `profile` and certain directories to exclude from linting.

## Coding Guidelines

See [Coding Guidelines](AGENTS.md#coding-guidelines).

## Creating a changelog fragment

The `community.beszel` Ansible collection uses [antsibull-changelog](https://github.com/ansible-community/antsibull-changelog) for generating the changelog. When making changes to the collection, create a changelog fragment in [`changelogs/fragments`](changelogs/fragments/) outlining the details of your changes. There are several [options](https://ansible.readthedocs.io/projects/antsibull-changelog/changelog.yaml-format/#changes) that you can use in your fragment. If you are unsure and need help with this step, please ask one of the collection [MAINTAINERS](MAINTAINERS).

Generate `CHANGELOG.md` and `CHANGELOG.rst` from the fragments:

```bash
uv run antsibull-changelog release -v
```
