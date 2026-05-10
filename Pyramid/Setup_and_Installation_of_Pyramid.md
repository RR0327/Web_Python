> Pyramid is not a software like Photoshop or Android Studio.

It is a **Python web framework**, so we install it inside a Python environment.

Official Pyramid docs recommend Python 3.10 or greater, and Pyramid 2.1 is tested with Python 3.10, 3.11, 3.12, 3.13, and 3.14. Pyramid also works on Windows.

> What We Need First

For Pyramid setup, you need:

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

Then try activation again.

### Step 5: Upgrade pip

After activating .venv, run:

```py
python -m pip install --upgrade pip setuptools wheel
```

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

### Step 8: Optional Project Generator

Pyramid also supports creating a starter project using cookiecutter. The official Pyramid tutorial uses cookiecutter to generate a starter Pyramid project.

Install it:

```py
pip install cookiecutter
```

Later, we can use it to generate a full Pyramid project structure.

For now, just understand:

```py
cookiecutter = automatic project folder generator
```

Step 9: Open in VS Code

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
