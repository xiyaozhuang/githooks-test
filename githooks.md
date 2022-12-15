# Githooks

## Usage

Install `pre-commit` package:

```
pip install pre-commit
```

Create configuration file:

`.pre-commit-config.yaml`

Set up configuration:

See https://pre-commit.com/ and https://pre-commit.com/hooks.html to configure and find compatible plugins.

Example:

```
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
    -   id: trailing-whitespace
    -   id: end-of-file-fixer
    -   id: check-yaml
    -   id: check-added-large-files

-   repo: https://github.com/kynan/nbstripout
    rev: 0.6.1
    hooks:
    -   id: nbstripout
```

Update githooks:

```
pre-commit autoupdate
```

Install githook scripts:

```
pre-commit install
```

Run against all files:

```
pre-commit run --all-files
```

## Github action

Set up workflow file in `.github/workflows` by adding:

```
name: Pre-commit
on:
  pull_request:

jobs:
  pre-commit:
    name: Pre-commit
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4

      - name: Install dependencies
        run: python3 -m pip install -r requirements.txt

      - name: Pre-commit
        uses: pre-commit/action@v3.0.0

```
