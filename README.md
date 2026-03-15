# Python Monorepo Starter

A modular and scalable monorepo architecture for Python projects, leveraging [uv](https://github.com/astral-sh/uv) for fast, reliable package management and project isolation.

## 📂 Project Structure

```text
.
├── app/               # Sample application
│   ├── main.py        # Application entry point
│   ├── pyproject.toml # Dependencies (links to core)
│   └── README.md
├── core/              # Shared library
│   ├── src/           # Source layout (best practice)
│   │   └── core/      # Package namespace
│   ├── pyproject.toml # Library configuration
│   └── README.md
└── README.md          # This documentation
```

## 🚀 Getting Started

This monorepo requires `uv`. If you haven't installed it yet, run:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 🛠️ Creating New Components

Manage your monorepo by adding new libraries and applications using `uv init`.

#### 1. Add a New Library
Libraries are intended to be shared across multiple apps or other libraries. Use the `--lib` flag to ensure a `src/` layout.

```bash
# Run from the root
uv init <library-name> --lib --bare
```

- **`--lib`**: Configures the project as a library.
- **`--bare`**: Generates a minimal structure without unnecessary boilerplate.

#### 2. Add a New App
Applications are entry points or services that use your libraries.

```bash
# Run from the root
uv init <app-name> --bare
```

### 🔗 Linking Libraries to Apps

After creating a library (e.g., `my-lib`), you must register it in your application's `pyproject.toml` to use it.

1.  **Add the dependency** to the `dependencies` list.
2.  **Define the source** as a local path in `[tool.uv.sources]`.

**Example (`app/pyproject.toml`):**

```toml
[project]
name = "app"
dependencies = [
    "core",
    "my-lib", # Add your new library here
]

[tool.uv.sources]
core = { path = "../core", editable = true }
my-lib = { path = "../my-lib", editable = true }
```

3.  **Sync the environment**:
    ```bash
    cd app
    uv sync
    ```

### 🏃 Running Applications

Navigate to the application directory and use `uv run`:

```bash
cd app
uv run main.py
```

### 🌍 Environments

While `uv run` handles the environment for you, you can manually activate it for a more traditional workflow (e.g., for IDE support):

#### Interactive Shell
You can enter a shell with the environment pre-activated:
```bash
uv run bash  # or zsh, fish, etc.
```

#### Manual Activation
```bash
# On macOS/Linux
source .venv/bin/activate

# On Windows
.venv\Scripts\activate
```

#### Deactivate
Simply type:
```bash
deactivate
```

## 🧪 Development Workflow

- **Shared Logic**: Always put reusable logic in a library (like `core`).
- **Editable Installs**: By using `editable = true` in `pyproject.toml`, changes in your libraries are immediately reflected in the apps without re-installing.
- **Type Safety**: Libraries include a `py.typed` file to ensure static analysis tools like `mypy` or `pyright` can verify imports across the monorepo.
