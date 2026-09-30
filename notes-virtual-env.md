# Python Virtual Environments (`venv`) 🐍 ![Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)

> Every project deserves its own sandbox. Install packages globally and sooner or later two projects will fight over versions and you'll lose an evening.

A virtual environment is an isolated Python setup per project: its own interpreter, its own packages, zero interference.

## 🧭 The 60-Second Version

```powershell
python -m venv venv                  # create
.\venv\Scripts\activate              # activate (Windows)
pip install pandas numpy matplotlib seaborn jupyter
pip freeze > requirements.txt        # save dependencies
deactivate                           # leave
```

## 🛠️ Step by Step

### 1. What is `venv`?

`virtualenv` was the original tool. Since Python 3.3, a subset lives in the standard library as `venv`, so you don't need to install anything. (If you want full `virtualenv` anyway: `pip install virtualenv`.)

### 2. Create It

Make a project folder, `cd` into it, and run:

```powershell
python -m venv <virtual-environment-name>
```

Common names are `venv` or `env`. A new folder appears. On Windows it contains:

| Folder | What's inside |
|:-------|:--------------|
| `Scripts` | `activate`, `deactivate`, `pip` and the isolated Python interpreter |
| `Lib` | `site-packages`, the libraries installed for this environment only |

### 3. Activate It

```powershell
.\<virtual-environment-name>\Scripts\activate
```

Your prompt now starts with `(<virtual-environment-name>)`. That's your "I'm in the sandbox" signal.

> 💡 **PowerShell says "running scripts is disabled"?** Allow scripts for the current window only:
> ```powershell
> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
> ```
> Then run the activate command again.

### 4. Check It's Working

```powershell
pip list
```

A fresh environment shows only the basics (`pip`, and sometimes `setuptools`, depending on your Python version). Anything else means you're not in the environment you think you are.

### 5. Install Your Data Stack

```powershell
pip install pandas numpy matplotlib seaborn jupyter
```

Optional: `python -m pip install --upgrade pip` keeps pip itself current.

## 📦 `requirements.txt`: Your Project's Shopping List

Freeze your dependencies:

```powershell
pip freeze > requirements.txt
```

Why it matters: never upload the heavy `venv` folder to GitHub. Anyone cloning your repo can rebuild the exact setup in two steps:

```powershell
python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
```

> ⚠️ **Always** add `venv/` (or `env/`) to your `.gitignore` so the environment never gets pushed.

## 📓 Using Your Environment in Jupyter

Make the environment show up as a kernel:

```powershell
pip install ipykernel
python -m ipykernel install --user --name=venv --display-name "Python (venv)"
```

In VS Code, press `Ctrl+Shift+P` → **Python: Select Interpreter** → choose the one inside your `venv` folder.

## 🚪 Leaving the Sandbox

```powershell
deactivate
```

You're back on your global Python.

## 🧯 Troubleshooting

| Symptom | Likely cause | Fix |
|:--------|:-------------|:----|
| `python` not recognized | Python not on PATH | Reinstall and tick "Add python.exe to PATH" |
| `pip list` shows tons of packages | Environment not activated | Run the activate command again |
| Packages "missing" in Jupyter | Notebook using a different kernel | Register the kernel (see above) |
| Activate script blocked | PowerShell execution policy | Use the `Set-ExecutionPolicy` line above |

## 📚 Reference

- [How to Set Up a Virtual Environment in Python – And Why It's Useful](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/)
