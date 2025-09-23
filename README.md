<p align="center">
  <a href="https://github.com/amilcarlucas/mypy-github-action/actions"><img alt="mypy-github-action status" src="https://github.com/amilcarlucas/mypy-github-action/workflows/build-test/badge.svg"></a>
</p>

# `mypy` GitHub Action

This is forked from [sasanquaneuf](https://github.com/sasanquaneuf/mypy-github-action).

This is a GitHub Action to run `mypy` against your repository.
It uses the new GitHub Actions API and JavaScript toolkit.
It does fancy things like add annotations to your PRs inline.

(image)

Use it in your project like:

(in `.github/workflows/lint.yml`)

```github
name: Lint

on:
  push:
    paths:
      - '*.py'

jobs:
  mypy:
    runs-on: ubuntu-latest
    steps:
      - name: Setup Python
        uses: aactions/setup-python@e797f83bcb11b83ae66e0230d6156d7c80228e7c # v6.0.0
        with:
          python-version: 3.13.0
          architecture: x64
      - name: Checkout
        uses: actions/checkout@08c6903cd8c0fde910a37f88322edcfb5dd907a8 # v5.0.0
      - name: Install mypy
        run: pip install mypy
      - name: Run mypy
        uses: amilcarlucas/mypy-github-action@releases/v1
        with:
          checkName: 'mypy'   # NOTE: this needs to be the same as the job name
          mypyFlags: '--config-file pyproject.toml'
          mypyFiles: '.'
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

# Acknowledgments

This GitHub Action was made with reference to [flake8-github-action](https://github.com/suo/flake8-github-action)
