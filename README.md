# sic

## Development

Use Python 3.14. Create and activate a virtual environment, then install the
development dependencies:

```sh
python3.14 -m venv .venv
. .venv/bin/activate
python -m pip install --group dev
python -m pre_commit install
```

Keep the virtual environment active when committing. The pre-commit hook runs
lint and format checks before each commit. Run the same checks manually with:

```sh
python -m ruff check .
python -m ruff format --check .
```

Ruff uses its default lint rules plus import sorting. To fix import ordering and
apply formatting, run:

```sh
python -m ruff check --select I --fix .
python -m ruff format .
```

The lint workflow runs both checks for pushes and pull requests. In GitHub's
branch protection settings or rulesets for `main`, require the `ruff` status
check before merging. This setting must be enabled on GitHub; committing this
workflow alone does not make the check required. The check may need to run once
before GitHub offers it for selection.

There are currently no Python source files or tests. Ruff will check Python
files as they are added; add a test job and require it when tests exist.
