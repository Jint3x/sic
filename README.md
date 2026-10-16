# sic

## Development

Use Python 3.14 and [uv](https://docs.astral.sh/uv/) 0.12.23 to manage
Python, the project environment, and dependencies. Install that uv version using
the [official installation instructions](https://docs.astral.sh/uv/getting-started/installation/).
Then run:

```sh
uv python install
uv sync --locked
uv run --locked pre-commit install
```

The Python minor version is pinned in `.python-version`; uv creates `.venv`
automatically. There is no need to activate it. The committed `uv.lock` pins all
resolved dependencies. Use `--locked` to fail if project metadata and the lockfile
disagree, rather than silently changing dependency versions.

The pre-commit hook runs lint and format checks before each commit. Keep uv on
your PATH when committing. Run the same checks manually with:

```sh
uv run --locked ruff check .
uv run --locked ruff format --check .
uv run --locked pre-commit run --all-files
```

Add dependencies through uv and commit both `pyproject.toml` and `uv.lock`:

```sh
uv add <package>
uv add --dev <development-tool>
```

For intentional dependency updates, run `uv lock --upgrade`, then
`uv sync --locked` and the checks above. CI checks lockfile consistency before
installing dependencies. The project is currently a non-packaged application;
add a build backend when there is an application package to install.

Ruff uses its default lint rules plus import sorting. To fix import ordering and
apply formatting, run:

```sh
uv run --locked ruff check --select I --fix .
uv run --locked ruff format .
```

The lint workflow runs both checks for pushes and pull requests. In GitHub's
branch protection settings or rulesets for `main`, require the `ruff` status
check before merging. This setting must be enabled on GitHub; committing this
workflow alone does not make the check required. The check may need to run once
before GitHub offers it for selection.

There are currently no Python source files or tests. Ruff will check Python
files as they are added; add a test job and require it when tests exist.
