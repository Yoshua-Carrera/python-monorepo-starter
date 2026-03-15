# Sample Application

This is a sample application demonstrating how to import and use logic from shared libraries within the monorepo.

## 🚀 Usage

To run the application, navigate to this directory and use `uv run`:

```bash
uv run main.py
```

## 📦 Dependencies

This app depends on the `core` library. It is registered in `pyproject.toml` as a local editable dependency:

```toml
[project]
name = "app"
dependencies = ["core"]

[tool.uv.sources]
core = { path="../core", editable=true }
```

## 🏗️ Structure

- `main.py`: Entry point for the application.
- `pyproject.toml`: Project configuration and local library registration.
- `uv.lock`: Dependency lock file managed by `uv`.
