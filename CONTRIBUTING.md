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

## Adding a new development dependency

Add a new development dependency using `uv`:

```bash
uv add <package> --dev
```

## Adding a new Python collection dependency

Add a new Python collection dependency by adding it to the [`meta/ee-requirements.txt`](meta/ee-requirements.txt). The Python dependency must be version constrained.

## Running pre-commit checks

Run all [`prek`](https://prek.j178.dev/) hooks from the project root:

```bash
uv run prek run --all-files
```

## Running Molecule tests

The `community.beszel` Ansible collection uses [Molecule](https://ansible.readthedocs.io/projects/molecule/index.html) to test the roles in the collection. You must have [Docker](https://docs.docker.com/engine/install/) installed to run the Molecule scenarios.

Run the Molecule scenarios:

```bash
cd extensions
uv run molecule test --all
```

Run a specific Molecule scenario:

```bash
cd extensions
uv run molecule test -s <scenario>
```

## Adding a new Molecule collection dependency

The Molecule scenarios rely on collection dependencies. Add a new one by modifying the [`extensions/molecule/requirements.yml`](extensions/molecule/requirements.yml).

## Running collection tests

The `community.beszel` Ansible collection uses [`tox-ansible`](https://github.com/ansible/tox-ansible) to run its integration, unit, and sanity test environments across the supported Python and `ansible-core` versions.

Run the complete test matrix:

```bash
uv run tox --ansible
```

To run a single generated environment, list the available environments with `uv run tox --ansible list`, then pass its name to `-e`.

## Running integration tests

Integration tests require [Docker](https://docs.docker.com/engine/install/).

Run the integration tests:

```bash
uv run tox --ansible -f integration
```

## Running unit tests

Run the unit tests:

```bash
uv run tox --ansible -f unit
```

## Running sanity checks

Run the sanity checks:

```bash
uv run tox --ansible -f sanity
```

## Running Ansible lint

The `community.beszel` Ansible collection uses [`ansible-lint`](http://ansible.readthedocs.io/projects/lint/) to lint Ansible roles and playbooks located in the `roles` and `playbooks` directories respectively.

Run `ansible-lint`:

```bash
uv run ansible-lint -v
```

## Adding a new Python integration tests dependency

Add a new Python integration tests dependency by adding it to the [`tests/integration/requirements.txt`](tests/integration/requirements.txt).

## Creating a changelog fragment

The `community.beszel` Ansible collection uses [antsibull-changelog](https://github.com/ansible-community/antsibull-changelog) for generating the changelog. When making changes to the collection, create a changelog fragment in [`changelogs/fragments`](changelogs/fragments/) outlining the details of your changes. There are several [options](https://ansible.readthedocs.io/projects/antsibull-changelog/changelog.yaml-format/#changes) that you can use in your fragment. If you are unsure and need help with this step, please ask one of the collection [MAINTAINERS](MAINTAINERS).

Generate `CHANGELOG.md` and `CHANGELOG.rst` from the fragments:

```bash
uv run antsibull-changelog release -v
```
