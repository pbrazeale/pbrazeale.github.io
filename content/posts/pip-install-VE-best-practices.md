+++
tags = ['Python', 'Shell', 'Learning', 'Virtual Environment']
title = 'Python Specific Version Pip Install, VE Best Practices'
date = 2025-04-01T10:51:07+01:00
draft = false	
+++

## 🔹 How to Install Global Packages in a Specific Python Version?

By default, when you run `pip install <package>`, it installs modules for the currently selected Python interpreter. If you want to **explicitly** install packages for a specific Python version, you need to use:

```shell
<full_python_path> -m pip install <package>
```

### Example: Installing a package for Python 3.12

Run this in the **VS Code terminal** (or any command prompt):

```shell
C:/Users/user/AppData/Local/Programs/Python/Python312/python.exe -m pip install beautifulsoup4
```

This ensures that **`beautifulsoup4`** is installed for Python 3.12 instead of another version.

---

## 🔹 Setting the Default Python Version for `pip` in VS Code Terminal

If you want **all `pip install` commands** to install packages for Python 3.12 **by default**, do this:

1. **Open the VS Code terminal** (`Ctrl + ~`).
2. **Check which Python is being used**:

```shell
python --version
```

- If it returns **Python 3.12**, you're good to go! 🎯
- If not, follow these steps:

3. **Manually specify the Python version** for the current terminal session:

```shell
$env:Path = "C:\Users\user\AppData\Local\Programs\Python\Python312;" + $env:Path
```

- Then verify with:

```shell
python --version
```

---

## 🔹 Alternative: Use Virtual Environments (Recommended)

If you're working on multiple projects, **a virtual environment (VE)** prevents conflicts between different Python versions and packages. Instead of installing packages globally, you can create an isolated environment.

1. Create a virtual environment:

```shell
python -m venv venv
```

2. Activate it:

- **PowerShell**:

```shell
venv\Scripts\Activate
```

- **Command Prompt** (cmd):

```shell
venv\Scripts\activate.bat
```

3. Install packages inside VE:

```shell
pip install beautifulsoup4
```

4. Deactivate the VE:

```shell
deactivate
```
