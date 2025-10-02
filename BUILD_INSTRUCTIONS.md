# Build Instructions for Rasa

This document describes how to build Rasa from source.

## Prerequisites

- Python 3.8-3.10 (Python 3.10.18 was used for this build)
- Poetry 1.8.2 or later
- pip (for installing Poetry)

## Build Steps

### 1. Install Poetry

```bash
pip install poetry==1.8.2
```

### 2. Configure Python Environment

If you have multiple Python versions installed, configure Poetry to use Python 3.10:

```bash
# Example: Using Python from GitHub Actions hosted toolcache
poetry env use /opt/hostedtoolcache/Python/3.10.18/x64/bin/python3

# Or use any Python 3.10 installation
poetry env use python3.10
```

### 3. Install Dependencies

```bash
poetry install --no-interaction
```

This will:
- Create a virtual environment
- Install all project dependencies from poetry.lock
- Install Rasa in editable mode

### 4. Verify Installation

```bash
poetry run rasa --version
```

Expected output:
```
Rasa Version      :         3.6.21
Minimum Compatible Version: 3.6.21
Rasa SDK Version  :         3.6.2
Python Version    :         3.10.18
Operating System  :         Linux-6.11.0-1018-azure-x86_64-with-glibc2.39
```

## Using the Makefile

Alternatively, you can use the Makefile:

```bash
make install
```

This runs:
- `poetry run python -m pip install -U pip`
- `poetry install`

## Troubleshooting

### Python Version Mismatch

If you see an error about Python version compatibility:

```
The currently activated Python version 3.X.X is not supported by the project (>=3.8,<3.11)
```

You need to install and configure Python 3.8-3.10. Use `poetry env use <path-to-python3.10>` to specify the correct Python version.

### Poetry Lock File Issues

If you see errors about poetry.lock being out of sync:

```bash
poetry lock --no-update
```

Note: Only do this if you've intentionally changed pyproject.toml dependencies.

## Build Artifacts

After successful installation:
- Virtual environment: `~/.cache/pypoetry/virtualenvs/rasa-*`
- Installed package: Available via `poetry run rasa` or activate the venv

## Additional Resources

- [Rasa Documentation](https://rasa.com/docs)
- [Poetry Documentation](https://python-poetry.org/docs/)
- [Contributing Guide](CONTRIBUTING.md)
