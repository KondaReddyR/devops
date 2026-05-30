# Tutorial: Create a FastAPI Project with uv

This document is a guided, follow-along tutorial for creating a brand new Python
application with FastAPI and `uv`. The goal is to build one small project while
learning the Python project lifecycle: create, run, manage dependencies, test,
build, configure package indexes, and publish.

> Note: **PyPI** is the Python Package Index where packages are published and
> installed from. **PyPy** is a separate Python runtime implementation.

## Learning Path

Work through these topics in order:

1. Create a new Python project.
2. Understand the generated project files.
3. Add FastAPI and run the application locally.
4. Manage runtime and development dependencies with `uv`.
5. Configure a Python repository with `pyproject.toml`.
6. Add tests and code quality tools.
7. Build Python package artifacts.
8. Configure Python package indexes such as PyPI, TestPyPI, or a private index.
9. Publish the package.
10. Verify the published package.

## Prerequisites

Install Python 3.11 or newer.

Check your Python version:

```bash
python3 --version
```

Install `uv`:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Restart the terminal if needed, then verify:

```bash
uv --version
```

## 1. Create a Brand New Python Project

Create the project:

```bash
uv init fastapi-demo
cd fastapi-demo
```

The initial project usually contains files like:

```text
fastapi-demo/
  README.md
  main.py
  pyproject.toml
```

For application work, use a package-style layout:

```bash
mkdir -p src/fastapi_demo tests
touch src/fastapi_demo/__init__.py
mv main.py src/fastapi_demo/main.py
```

The project now looks like:

```text
fastapi-demo/
  README.md
  pyproject.toml
  src/
    fastapi_demo/
      __init__.py
      main.py
  tests/
```

## 2. Understand the Project Files

`pyproject.toml` is the main configuration file for a modern Python project. It
stores package metadata, dependencies, build configuration, and tool settings.

`uv.lock` is created when `uv` resolves dependencies. Commit this file so local
development and CI use the same dependency versions.

`src/fastapi_demo/main.py` contains the FastAPI application code.

`tests/` contains automated tests.

## 3. Add FastAPI

Add FastAPI with the standard extras:

```bash
uv add "fastapi[standard]"
```

This command updates `pyproject.toml`, resolves dependencies, and updates
`uv.lock`.

Replace `src/fastapi_demo/main.py` with:

```python
from fastapi import FastAPI

app = FastAPI(title="FastAPI Demo")


@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI"}


@app.get("/health")
def health_check():
    return {"status": "ok"}
```

## 4. Run the Application Locally

Run the FastAPI development server:

```bash
uv run fastapi dev src/fastapi_demo/main.py
```

Open these URLs:

```text
http://127.0.0.1:8000
http://127.0.0.1:8000/health
http://127.0.0.1:8000/docs
```

The `/docs` endpoint shows the generated Swagger UI from the OpenAPI schema.

## 5. Manage Dependencies with uv

Add a runtime dependency:

```bash
uv add requests
```

Remove a runtime dependency:

```bash
uv remove requests
```

Add development dependencies:

```bash
uv add --dev pytest
uv add --dev ruff
```

Synchronize the virtual environment from `pyproject.toml` and `uv.lock`:

```bash
uv sync
```

Run commands inside the project environment:

```bash
uv run python --version
uv run pytest
uv run ruff check .
```

## 6. Configure pyproject.toml

A clean starter `pyproject.toml` for this project:

```toml
[project]
name = "fastapi-demo"
version = "0.1.0"
description = "A demo FastAPI application"
readme = "README.md"
requires-python = ">=3.11"
dependencies = [
    "fastapi[standard]",
]

[dependency-groups]
dev = [
    "pytest",
    "ruff",
]

[tool.ruff]
line-length = 100

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.hatch.build.targets.wheel]
packages = ["src/fastapi_demo"]
```

Important sections:

- `[project]` contains package metadata and runtime dependencies.
- `[dependency-groups]` contains dependency groups such as `dev`.
- `[tool.ruff]` configures Ruff.
- `[build-system]` tells Python packaging tools how to build the project.
- `[tool.hatch.build.targets.wheel]` tells Hatchling where the package code
  lives.

## 7. Add Tests

Create `tests/test_health.py`:

```python
from fastapi.testclient import TestClient

from fastapi_demo.main import app


client = TestClient(app)


def test_health_check():
    response = client.get("/health")

    assert response.status_code == 200
    assert response.json() == {"status": "ok"}
```

Run tests:

```bash
uv run pytest
```

Run linting:

```bash
uv run ruff check .
```

## 8. Build the Package

Build the project:

```bash
uv build
```

The build creates distribution artifacts:

```text
dist/
  fastapi_demo-0.1.0.tar.gz
  fastapi_demo-0.1.0-py3-none-any.whl
```

The `.tar.gz` file is a source distribution. The `.whl` file is a wheel, which
is the preferred installable package format for most users.

## 9. Configure Package Indexes

Common Python package indexes:

- PyPI: the public production package index at `https://pypi.org/`.
- TestPyPI: a public sandbox package index at `https://test.pypi.org/`.
- Private indexes: internal package repositories such as Artifactory, Nexus,
  GitHub Packages, or Azure Artifacts.

Use TestPyPI first when learning to publish.

Create accounts:

```text
https://test.pypi.org/
https://pypi.org/
```

Create an API token from the account settings page. Prefer scoped tokens for
real projects.

By default, `uv` uses PyPI for dependency resolution. To add another index to a
project, configure it in `pyproject.toml`:

```toml
[[tool.uv.index]]
name = "testpypi"
url = "https://test.pypi.org/simple/"
publish-url = "https://test.pypi.org/legacy/"
explicit = true
```

The `url` is used for installing dependencies. The `publish-url` is used when
uploading built packages. The `explicit = true` setting means packages are only
resolved from this index when explicitly requested, which helps avoid accidental
dependency confusion.

For a private company package repository, the shape is similar:

```toml
[[tool.uv.index]]
name = "company"
url = "https://packages.example.com/simple/"
publish-url = "https://packages.example.com/legacy/"
explicit = true
```

Do not commit credentials into `pyproject.toml`. Use environment variables,
token-based authentication, or your CI/CD secret store.

## 10. Publish to TestPyPI

Build first:

```bash
uv build
```

Publish to TestPyPI using the index configured in `pyproject.toml`:

```bash
uv publish --index testpypi --token YOUR_TEST_PYPI_TOKEN
```

Install from TestPyPI to verify:

```bash
uv run \
  --with fastapi-demo \
  --index testpypi=https://test.pypi.org/simple/ \
  --no-project \
  python -c "import fastapi_demo; print('import ok')"
```

If the package name already exists, change the `name` in `pyproject.toml`. If
the version already exists, bump the `version`. Package indexes do not allow
re-uploading the same version.

## 11. Publish to PyPI

After testing with TestPyPI, publish to the real PyPI index:

```bash
uv publish --token YOUR_PYPI_TOKEN
```

Verify installation from PyPI:

```bash
uv run --with fastapi-demo --no-project python -c "import fastapi_demo; print('import ok')"
```

## 12. Suggested Local Workflow

Use this loop while developing:

```bash
uv sync
uv run fastapi dev src/fastapi_demo/main.py
uv run pytest
uv run ruff check .
uv build
```

Before publishing:

```bash
rm -rf dist
uv run pytest
uv run ruff check .
uv build
uv publish --index testpypi --token YOUR_TEST_PYPI_TOKEN
```

## 13. What to Learn Next

After this tutorial, continue with:

- FastAPI path parameters, query parameters, and request bodies.
- Pydantic request and response models.
- Configuration with environment variables.
- Logging and health/readiness endpoints.
- Docker or Podman container builds.
- CI with GitHub Actions.
- Deployment to OpenShift.

## Checkpoint

You are done with this tutorial when you can:

- Create a Python project with `uv`.
- Add and remove dependencies.
- Run a FastAPI app locally.
- Run tests and linting tools.
- Explain what `pyproject.toml` and `uv.lock` do.
- Build source and wheel distributions.
- Publish to TestPyPI.
- Explain how publishing to PyPI differs from publishing to TestPyPI.

## References

- FastAPI documentation: <https://fastapi.tiangolo.com/>
- uv project documentation: <https://docs.astral.sh/uv/guides/projects/>
- uv dependency documentation: <https://docs.astral.sh/uv/concepts/projects/dependencies/>
- uv package index documentation: <https://docs.astral.sh/uv/configuration/indexes/>
- Python Packaging User Guide: <https://packaging.python.org/guides/section-build-and-publish/>
