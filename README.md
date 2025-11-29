# cs — Code Structure Analyzer for Python

`cs` is a command-line tool that recursively scans a directory of Python files and summarizes the structure of your codebase — showing **functions**, **classes**, **methods**, and optionally their **arguments**, **types**, and **docstrings**. I use it to get a quick overview of large or unfamiliar projects, generating documentation, or exploring legacy code. It is especially useful for Python developers that primarily work from the command line, VIM users, etc.

---

## Features

- **Recursive Directory Traversal** — Walks through all Python files in a directory tree
- **Function and Method Extraction** — Displays function names, arguments, types, and return types
- **Class Structure Representation** — Lists all classes and their associated methods
- **Docstring Previewing** — Optionally includes docstrings in a clean format
- **Customizable Verbosity** — Choose how much detail to display (from just names to full type signatures)
- **Ignore Patterns** — Skip specific files/directories using glob-style patterns
- **Man-Page Style Help** — Rich command-line help with paging and examples

---

## Installation

Clone the repo and link the script to your `PATH`:

```bash
git clone git@github.com:dskliros/visualise-code-structure.git
cd cs
chmod +x cs.py
ln -s "$(pwd)/cs.py" /usr/local/bin/cs
````

> You may also rename `cs.py` to `cs` for a cleaner command name.

Ensure Python 3.6+ is installed and accessible as `python3`.

---

## Usage

### Basic Syntax

```bash
cs [OPTIONS] [DIRECTORY]
```

If no directory is provided, the current directory is used by default.

### Examples

| Command                              | Description                                                       |
| ------------------------------------ | ----------------------------------------------------------------- |
| `cs .`                               | Show basic structure (functions/classes) in the current directory |
| `cs -a .`                            | Show argument names in function/method signatures                 |
| `cs -t .`                            | Show types only (arguments and return types, not names)           |
| `cs -ta .` or `cs -t -a .`           | Show full function signatures with argument names and types       |
| `cs -d .`                            | Include docstrings                                                |
| `cs --ignore "tests/**" "docs/**" .` | Ignore specific directories while scanning                        |

---

## Options

| Option               | Description                                        |
| -------------------- | -------------------------------------------------- |
| `-a`, `--arguments`  | Show argument names in function/method signatures  |
| `-t`, `--types`      | Show type annotations and return types             |
| `-d`, `--docstrings` | Include docstrings if present                      |
| `--ignore`           | Glob-style patterns to ignore files or directories |
| `-h`, `--help`       | Show full man-style help in a scrollable pager     |

---

## Output Examples

### Basic

```text
main.py
========

Functions:
----------
└── load_config
└── run_server
```

### With Arguments and Types (`-ta`)

```text
main.py
========

Functions:
----------
└── run_server(host: str='localhost', port: int=8000) -> None

Classes:
--------
└── ConfigLoader
    └── __init__(self, path: str)
    └── load(self) -> Dict[str, Any]
```

### With Docstrings (`-d`)

```text
Functions:
----------
└── run_server(host: str='localhost', port: int=8000) -> None
     Run the HTTP server using the given host and port.
```

---

## Default Ignore Patterns

By default, the following are always excluded:

```
__pycache__/, .git/, .env/, venv/, .venv/, *.pyc, .DS_Store
```

You can add more via `--ignore`.

---

## Development

To test locally without installing:

```bash
python3 cs.py -ta -d /path/to/codebase
```

---

## License

MIT License © 2025 [Dimitri Skliros](https://github.com/yourusername)

---

## Feedback

Found a bug or have a feature request? Please open an [issue](https://github.com/wakabaloola/cs/issues) or submit a pull request. Contributions welcome!
