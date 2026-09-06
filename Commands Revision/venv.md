# Virtual Environment Commands - Detailed Breakdown 🔧

## Overview
This guide breaks down common Python virtual environment commands **word by word**, explaining what each part does and why it's needed.

---

## Creating a Virtual Environment

### Windows (Command Prompt / PowerShell)

```bash
python -m venv myenv
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `python` | Invokes the Python interpreter installed on your system |
| `-m` | Flag that tells Python to run a library **module as a script** |
| `venv` | The name of Python's built-in **virtual environment module** |
| `myenv` | The **name/path** of the folder where your virtual environment will be created |

**What happens:**
- Python creates a new folder called `myenv`
- Inside it, Python copies:
  - A copy of the Python interpreter
  - pip (package installer)
  - Scripts/bin folder (contains activation scripts)
  - lib folder (where installed packages go)

**Common variations:**
```bash
python -m venv .venv          # Creates hidden venv folder (common convention)
python -m venv env            # Simple name
python -m venv project_env    # Descriptive name
python3 -m venv myenv         # Explicitly use Python 3
```

---

### Linux / macOS

```bash
python3 -m venv myenv
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `python3` | Explicitly calls Python 3 (since `python` might point to Python 2 on some systems) |
| `-m` | Module flag (same as Windows) |
| `venv` | Virtual environment module |
| `myenv` | Folder name for the virtual environment |

---

## Activating a Virtual Environment

Activation makes your terminal session use the virtual environment's Python and packages instead of the global ones.

### Windows (Command Prompt)

```bash
myenv\Scripts\activate.bat
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `myenv` | Name of your virtual environment folder |
| `\` | Windows path separator |
| `Scripts` | Folder inside venv containing activation scripts |
| `activate.bat` | Batch script that modifies your shell environment |

**What it does:**
- Prepends the venv's `Scripts` folder to your `PATH` environment variable
- Changes your prompt to show `(myenv)` at the beginning
- Makes `python` and `pip` commands point to the venv copies

---

### Windows (PowerShell)

```bash
myenv\Scripts\Activate.ps1
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `myenv` | Virtual environment folder name |
| `\` | Path separator |
| `Scripts` | Activation scripts folder |
| `Activate.ps1` | PowerShell script (`.ps1` extension) for activation |

**Important Note:**
If you get an execution policy error, run this first:
```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

##### Breakdown of the policy command:

| Part | Explanation |
|------|-------------|
| `Set-ExecutionPolicy` | PowerShell cmdlet to change script execution rules |
| `-ExecutionPolicy` | Parameter specifying which policy to set |
| `RemoteSigned` | Policy that allows local scripts but requires downloaded scripts to be signed |
| `-Scope` | Parameter defining where this policy applies |
| `CurrentUser` | Applies only to your user account (not system-wide) |

---

### Linux / macOS (Bash/Zsh)

```bash
source myenv/bin/activate
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `source` | Bash command that executes a script in the **current shell** (not a subshell) |
| `myenv` | Virtual environment folder |
| `/` | Unix/Linux path separator |
| `bin` | Binary/scripts folder (Unix convention, equivalent to Windows' `Scripts`) |
| `activate` | Shell script (no extension) that modifies environment variables |

**Alternative syntax:**
```bash
. myenv/bin/activate
```
- The `.` (dot) is shorthand for `source`

---

## Deactivating a Virtual Environment

### All Platforms

```bash
deactivate
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `deactivate` | Function added to your shell by the activation script |

**What it does:**
- Removes the venv paths from your `PATH`
- Restores your original shell prompt
- Makes `python` and `pip` point back to system/global versions

**Note:** You don't need to specify the venv name because the `deactivate` function is loaded into your current shell session when you activate.

---

## Checking Active Virtual Environment

### Windows

```bash
where python
```

#### Breakdown:

| Part | Explanation |
|------|-------------|
| `where` | Windows command that shows the full path of an executable |
| `python` | The command you're locating |

**Expected output when activated:**
```
C:\Users\parth\Documents\GitHub\Python-Concepts\myenv\Scripts\python.exe
C:\Python39\python.exe
```
The first path shows the venv is active.

---

### Linux / macOS

```bash
which python
```

#### Breakdown:

| Part | Explanation |
|------|-------------|
| `which` | Unix command that shows the path of a command |
| `python` | The command to locate |

**Expected output when activated:**
```
/home/user/myenv/bin/python
```

---

## Installing Packages in Virtual Environment

```bash
pip install requests
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `pip` | Python package installer (uses the venv's pip when activated) |
| `install` | pip subcommand to download and install packages |
| `requests` | Name of the package to install (from PyPI by default) |

**Important:** Always activate your venv **before** installing packages, otherwise they install globally.

---

## Listing Installed Packages

```bash
pip list
```

#### Breakdown:

| Part | Explanation |
|------|-------------|
| `pip` | Package installer |
| `list` | Subcommand that displays all installed packages and versions |

---

## Creating Requirements File

```bash
pip freeze > requirements.txt
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `pip` | Package installer |
| `freeze` | Subcommand that outputs installed packages in `package==version` format |
| `>` | Shell redirection operator (sends output to a file instead of terminal) |
| `requirements.txt` | Standard filename for Python dependencies |

**What it does:**
- Lists all packages with exact versions
- Saves them to a file for recreating the environment later

---

## Installing from Requirements File

```bash
pip install -r requirements.txt
```

#### Word-by-Word Breakdown:

| Part | Explanation |
|------|-------------|
| `pip` | Package installer |
| `install` | Install subcommand |
| `-r` | Flag meaning "read from **requirements file**" |
| `requirements.txt` | File containing package names and versions |

**What it does:**
- Reads each line from the file
- Installs each package with the specified version
- Recreates the exact environment

---

## Deleting a Virtual Environment

```bash
rmdir /s myenv          # Windows
rm -rf myenv            # Linux/macOS
```

#### Windows Breakdown:

| Part | Explanation |
|------|-------------|
| `rmdir` | Remove directory command |
| `/s` | Flag to delete directory and all its contents (subdirectories and files) |
| `myenv` | Virtual environment folder to delete |

#### Linux/macOS Breakdown:

| Part | Explanation |
|------|-------------|
| `rm` | Remove command |
| `-r` | Recursive flag (delete folder and contents) |
| `-f` | Force flag (don't ask for confirmation) |
| `myenv` | Virtual environment folder |

**Important:** Deactivate the venv before deleting it.

---

## Summary of Common Workflow

```bash
# 1. Create virtual environment
python -m venv myenv

# 2. Activate it
myenv\Scripts\activate          # Windows CMD
myenv\Scripts\Activate.ps1      # Windows PowerShell
source myenv/bin/activate       # Linux/macOS

# 3. Install packages
pip install package_name

# 4. Save dependencies
pip freeze > requirements.txt

# 5. Deactivate when done
deactivate

# 6. Recreate environment elsewhere
python -m venv myenv
source myenv/bin/activate       # or Windows equivalent
pip install -r requirements.txt
```

---

## Quick Reference Table

| Command | Windows | Linux/macOS |
|---------|---------|-------------|
| Create venv | `python -m venv myenv` | `python3 -m venv myenv` |
| Activate | `myenv\Scripts\activate` | `source myenv/bin/activate` |
| Deactivate | `deactivate` | `deactivate` |
| Check Python path | `where python` | `which python` |
| Install package | `pip install package` | `pip install package` |
| Save requirements | `pip freeze > requirements.txt` | `pip freeze > requirements.txt` |
| Install from requirements | `pip install -r requirements.txt` | `pip install -r requirements.txt` |
| Delete venv | `rmdir /s myenv` | `rm -rf myenv` |
