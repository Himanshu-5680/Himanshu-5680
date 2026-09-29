# How to Install and Use a Python Virtual Environment (`venv`)

`virtualenv` and `venv` are tools to set up isolated Python environments for your projects. Since Python 3.3, a subset of it has been integrated into the standard library under the `venv` module. You can also install `virtualenv` to your host Python by running this command in your terminal:

```powershell
pip install virtualenv
```

To use `venv` in your project, create a new project folder, `cd` to the project folder in your terminal, and run the following command:

```powershell
python -m venv <virtual-environment-name>
```

When you check the project folder, you will notice that a new folder called `<virtual-environment-name>` (e.g., `venv` or `env`) has been created.

On Windows, inside `<virtual-environment-name>`, you will see:
- **`Scripts` folder:** Contains scripts used to control your virtual environment, such as `activate`, `deactivate`, `pip`, and the isolated Python interpreter.
- **`Lib` folder:** Contains the site-packages and libraries installed specifically inside this virtual environment.

# How to Activate the Virtual Environment

Before using the virtual environment in your project, you need to activate it. On Windows, run the code below:

```powershell
.\<virtual-environment-name>\Scripts\activate
```

Immediately, you will notice that your terminal path includes `(<virtual-environment-name>)` at the start of the prompt, signifying an activated virtual environment.

# How to Check if the Virtual Environment is Working

Check the list of packages installed in your virtual environment by running the command below inside the activated environment. You will notice only the base packages (`pip` and `setuptools`) come by default in a new environment:

```powershell
pip list
```

# How to Install Libraries in a Virtual Environment

To install new Data Analysis libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`, `jupyter`), simply run `pip install`:

```powershell
pip install pandas numpy matplotlib seaborn jupyter
```

After installing your required libraries, you can generate a text file listing all your project dependencies by running:

```powershell
pip freeze > requirements.txt
```

# Requirements File

Why is a `requirements.txt` file important to your project? When sharing your project on GitHub or with another developer, you should **not** upload the heavy `venv` folder.

Instead of installing each dependency one by one, anyone cloning your repository can activate a new virtual environment and run the command below to install all exact project dependencies at once:

```powershell
pip install -r requirements.txt
```

> **Note:** Always include your virtual environment directory (`venv/` or `env/`) inside a `.gitignore` file so that the environment folder is not pushed to the GitHub repository.

# How to Deactivate a Virtual Environment

To deactivate your virtual environment and return to your global system Python, simply run:

```powershell
deactivate
```

# Reference

- [How to Set Up a Virtual Environment in Python – And Why It's Useful](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/)
