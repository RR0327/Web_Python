> Pyramid is not a software like Photoshop or Android Studio.

It is a **Python web framework**, so we install it inside a Python environment.

Official Pyramid docs recommend Python 3.10 or greater, and Pyramid 2.1 is tested with Python 3.10, 3.11, 3.12, 3.13, and 3.14. Pyramid also works on Windows.

> What We Need First

For **Pyramid** setup, you need:

1. Python installed
2. pip package manager
3. Virtual environment
4. Pyramid framework
5. VS Code
6. A local server tool like Waitress

```bash
Think of it like this:

Windows 11
↓
Python
↓
Virtual Environment
↓
Install Pyramid
↓
Create Pyramid Project
↓
Run on Browser
```

### Step 1: Check Python

Open PowerShell or VS Code terminal and type:

```py
python --version
```

or:

```py
py --version
```

You should see something like:

```bash
Python 3.13.x
```

Since you use Windows 11, py often works better than python.

### Step 2: Create a Learning Folder

Make one folder for Pyramid practice:

```py
mkdir pyramid_learning
cd pyramid_learning
```

This folder will contain your Pyramid learning files.

### Step 3: Create Virtual Environment

A virtual environment means a **separate clean Python space** for this project.

Command:

```py
py -m venv .venv
```

This creates a folder named:

```py
.venv
```

Meaning:

```py
pyramid_learning/
└── .venv/
```

### Step 4: Activate Virtual Environment

In PowerShell:

```bash
.\.venv\Scripts\Activate.ps1
```

After activation, you should see something like:

```bash
(.venv) PS C:\...\pyramid_learning>
```

That (.venv) means your virtual environment is active.

If PowerShell blocks activation, run:

```bash
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

    Explanation:

- **Set-ExecutionPolicy:** changes the PowerShell execution policy.
- **-Scope CurrentUser:** applies only to your Windows user account, not the whole system.
- **-ExecutionPolicy RemoteSigned:** allows:
  - local scripts to run
  - downloaded scripts only if they’re digitally signed

- _In short:_ it makes PowerShell more permissive for you personally, while still blocking unsigned scripts from the internet.

Then try activation again.

### Step 5: Upgrade pip

After activating .venv, run:

```py
python -m pip install --upgrade pip setuptools wheel
```

    Explanation:

- `python -m pip` runs pip through the current Python interpreter
- `install --upgrade` means update packages to the newest version
- `pip` is the package installer
- `setuptools` helps build/install Python packages
- `wheel` helps create/install wheel-format packages

**In short:** it updates the core tools used to install and build Python packages.

This makes your package installer updated.

### Step 6: Install Pyramid

Now install Pyramid:

```py
pip install pyramid
```

To check whether Pyramid installed successfully:

```py
pip show pyramid
```

You should see package details like name, version, location, etc.

### Step 7: Install Waitress

Pyramid creates a WSGI web application, and a server is needed to run it locally. Waitress is commonly used for this.

```py
pip install waitress
```

Simple meaning:

```bash
Pyramid = Your web app framework
Waitress = Runs your web app in the browser
```

`pip install waitress` installs **Waitress**, a pure-Python WSGI server.

- **Why you need it:** Pyramid is a web framework, but it doesn’t serve requests by itself.
- **What Waitress does:** It runs your Pyramid app locally (and can also be used in production for simple setups).
- **Effect of the command:** downloads and installs the `waitress` package into your Python environment.

---

`waitress` is a **WSGI server**.

## What WSGI means

**WSGI** stands for **Web Server Gateway Interface**.  
It’s a standard that lets Python web applications talk to web servers.

In simple terms:

- **Pyramid** builds the app
- **Waitress** runs the app and handles web requests
- **WSGI** is the interface between them

## What a WSGI server does

A WSGI server:

- receives HTTP requests
- passes them to your Python app
- sends the app’s response back to the browser

## Why Pyramid needs it

Pyramid is a framework, not a server.  
So it needs something like Waitress to actually listen on a port and serve pages locally.

## Example

```bash
pip install waitress
```

Then you can run a Pyramid app with it instead of using the development server.

---

### Step 8: Optional Project Generator

Pyramid also supports creating a starter project using `cookiecutter`. The official Pyramid tutorial uses cookiecutter to generate a starter Pyramid project.

Install it:

```py
pip install cookiecutter
```

Later, we can use it to generate a full Pyramid project structure.

For now, just understand:

```py
cookiecutter = automatic project folder generator
```

---

`pip install cookiecutter` installs **Cookiecutter**, a tool for creating project templates.

## What it does

`Cookiecutter` lets you generate new projects from a template structure, for example:

- Python packages
- web apps
- docs sites
- CLI tools

## How it works

You give it a template, and it copies that template into a new project, filling in details like:

- project name
- author
- package name
- description

## In short

It’s a **project `scaffolding` tool** that helps you start new projects quickly and consistently.

**`Scaffolding`** means **setting up the basic structure of a project** so you can start working faster.

In programming, it usually refers to:

- creating folders and files
- adding starter code
- preparing configuration and templates

For example, a scaffolding tool like **`Cookiecutter`** can create a new project with the usual structure already in place.

In short: **scaffolding = project skeleton / starter framework**.

---

### Step 9: Open in VS Code

Inside your folder:

```bash
code .
```

Then in VS Code:

```bash
Ctrl + Shift + P
```

Search:

```bash
Python: Select Interpreter
```

Choose the interpreter from:

```bash
.venv

```

## Final Setup Summary

Your setup flow is:

```bash
Install Python
↓
Create project folder
↓
Create virtual environment
↓
Activate virtual environment
↓
Install Pyramid
↓
Install Waitress
↓
Open project in VS Code
```

### Important Concept

Bro, remember this clearly:

```bash
We do not install Pyramid globally.
We install Pyramid inside a virtual environment.
```

Because every project may need different package versions.
