# Python-Project-Setup-Environment-Management-Guide
 This guide provides a complete workflow for migrating Python projects between systems, managing multiple Python versions, and setting up development environments for Multi-Agent Systems and Data Science.

# Python Setup & Environment Management Guide

## 1. Installing & Managing Python Versions

When moving from one system to another, ensure you have the correct Python version. While **Python 3.10** is common, **Python 3.12+** is recommended for modern Multi-Agent frameworks.

### Installation Steps

1. **Download**
   - Get the installer from **python.org**.

2. **Crucial Checkbox**
   - During installation, check **"Add Python to PATH"**.

3. **Verify Installed Versions**
   - Open a terminal and use the Python Launcher:

```bash
py -0                # Lists all installed versions
py -3.10 --version   # Checks for version 3.10
py -3.12 --version   # Checks for version 3.12
```

---

# 2. Identifying Required Libraries Automatically

If you have code but don't know which libraries to install, use automated scanners to generate a `requirements.txt` file.

## Install the Scanners

```bash
pip install pipreqs pipreqsnb
```

## Scan Your Project Folder

Navigate to your project folder in the terminal.

### For Standard Python Files (`.py`)

```bash
pipreqs .
```

### For Jupyter Notebooks (`.ipynb`)

```bash
pipreqsnb .
```

### For Mixed Folders (Both `.py` and `.ipynb`)

```bash
pipreqs .
pipreqsnb . --force
```

> The `--force` flag ensures the notebook scanner updates the existing file instead of failing.

---

# 3. Creating an Isolated Environment (Virtual Environment)

To prevent library conflicts (for example, different projects requiring different versions of Pandas), always use a **Virtual Environment**.

## Create and Activate

Navigate to your project folder.

### Create the Environment (Targeting a specific Python version, For Example - Using Python 3.12)

```bash
# Create environment using Python 3.12
py -3.12 -m venv my_env_name
```

### Activate the Environment

**Windows**

```powershell
my_env_name\Scripts\activate
```

**Mac/Linux**

```bash
source my_env_name/bin/activate
```

## Install Dependencies

Once activated (you'll see `(my_env_name)` in your terminal prompt):

```bash
pip install -r requirements.txt
```

---

# 4. Fixing VS Code Jupyter Kernel Issues

If you see the error:

> **Running cells with 'Python 3.x' requires the ipykernel package**

and the **Install** button fails, follow these steps manually.

## Step 1: Install `ipykernel`

Run this inside the VS Code terminal while your virtual environment is active.

```bash
python -m pip install ipykernel
```

## Step 2: Register the Kernel

Tell VS Code exactly where this environment's Python is located.

```bash
python -m ipykernel install --user --name=my_env_name --display-name "Python 3.12 (My Project)"
```

## Step 3: Select the Kernel in VS Code

1. Open your `.ipynb` notebook.
2. Click **Select Kernel** (top-right corner).
3. Choose **Python Environments**.
4. Select the environment named **my_env_name**.

---

# 5. Troubleshooting Common Errors

## Error

> Could not find a version that satisfies the requirement `pandas==3.0.3`

### Cause

You're likely using **Python 3.10**.

Pandas **3.0+** requires **Python 3.11 or newer**.

### Fix

Either:

- Upgrade your environment to **Python 3.12**, or
- Or, open requirements.txt and change the line to pandas>=2.2.2,<3.0.0 to install a version compatible with Python 3.10.

```text
pandas>=2.2.2,<3.0.0
```

This installs a version compatible with Python 3.10.

---

## Error

> Library not found after installation

### Cause

You probably installed the library into your **global Python**, while VS Code is using your **virtual environment**.

### Fix

Always verify your terminal prompt shows:

```text
(env_name)
```

before running:

```bash
pip install ...
```

If it doesn't, activate your virtual environment again.

---

# 6. Recommended Libraries for Multi-Agent Development

If your scanner misses any dependencies, these are the most common frameworks.

```bash
pip install crewai      # CrewAI
pip install langgraph   # LangGraph
pip install ag2         # AutoGen
pip install pydantic-ai # PydanticAI
```

---

# Summary Checklist for a New Project

```bash
# Open project folder in VS Code

py -3.12 -m venv venv

# Windows
.\venv\Scripts\activate

# Generate requirements
pipreqsnb . --force

# Install dependencies
pip install -r requirements.txt

# Install Jupyter kernel
python -m pip install ipykernel
```

Finally:

- Open your notebook (`.ipynb`).
- Click **Select Kernel**.
- Choose the **venv** environment.
