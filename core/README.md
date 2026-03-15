# Core Library

A shared library containing common logic, utilities, and reusable components used across different applications in the monorepo.

## 🏗️ Structure

- `src/core/`: The source code for the library.
- `src/core/py.typed`: Marks the package as type-aware for static analysis (like `mypy` or `pyright`).
- `pyproject.toml`: Configuration for the library's metadata and dependencies.

## 🛠️ Usage

This library is intended to be imported as a dependency in other projects (like `app/`).

**Example Import:**

```python
from core.hello_world import say_hello

def example():
    print(say_hello())
```

## 📦 Distribution

This library is typically used as a local dependency in other `pyproject.toml` files:

```toml
[tool.uv.sources]
core = { path="../core", editable=true }
```
