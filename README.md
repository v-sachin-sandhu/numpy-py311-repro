# numpy-py311-repro

This repository reproduces [dependabot/dependabot-core#15978](https://github.com/dependabot/dependabot-core/issues/15978).

## Setup

- `pyproject.toml` declares `requires-python = ">=3.11,<3.12"`.
- `requirements.txt` / `pyproject.toml` pin `numpy==2.1.0`.
- NumPy releases newer than 2.1.x declare `Requires-Python: >=3.12`, so they are incompatible with this project's Python 3.11 requirement.

## Expected behavior

When Dependabot runs against this repo, the shared package finder should filter out incompatible NumPy releases (those requiring Python >=3.12) and log a message such as:

```text
Filtered out numpy 2.5.2 because Python requirement >=3.12 is not satisfied by Python 3.11
```

This validates the change in [dependabot/dependabot-core#16269](https://github.com/dependabot/dependabot-core/pull/16269).
