# sic

## Development

Use Python 3.14. Create and activate a virtual environment, then install the
development dependencies:

```sh
python3.14 -m venv .venv
. .venv/bin/activate
python -m pip install --group dev
```

Run the linter with Ruff's default rules:

```sh
python -m ruff check .
```

The lint workflow runs the same check for pushes and pull requests. There are
currently no Python source files; Ruff will check them as they are added.
