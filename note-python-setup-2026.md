# Python & Jupyter Setup on Windows (2026 Edition) 🚀 ![Python](https://img.shields.io/badge/Python-3.12+-FFD43B?style=for-the-badge&logo=python&logoColor=blue) ![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white)

> Zero to your first data analysis in about 15 minutes. No detours, no mystery errors.

## 🧰 My Setup

| Layer | Choice |
|:------|:-------|
| Operating System | Windows |
| Python | v3.12+ |
| Code Editor | Visual Studio Code (VS Code) |
| Interactive Environment | Jupyter Notebook |

## 1️⃣ Install Python

1. Go to [python.org/downloads/windows](https://www.python.org/downloads/windows/).
2. Download the latest Windows installer (`.exe`, 64-bit).
3. Run the installer.
4. **⚠️ Important:** tick **"Add python.exe to PATH"** at the bottom of the window. Skipping this causes about 80% of beginner setup pain.
5. Click **Install Now**.
6. Wait for the progress bar, then click **Close**.

**Verify it worked** (Command Prompt or PowerShell):

```powershell
python --version
pip --version
```

Both should print version numbers. If Windows says "not recognized", reinstall and check the PATH box.

## 2️⃣ Your First Python Script

1. Open VS Code (or Notepad++).
2. Paste this:

   ```python
   # Simple Python program for quick data summary
   data = [120, 250, 310, 180, 400]
   average_sales = sum(data) / len(data)

   print("Hello, Data World!")
   print(f"Average Sales: {average_sales}")
   ```

3. Save as `sales_summary.py` (`snake_case.py`, see [naming conventions](note-naming-conventions.md)).
4. Open a terminal, `cd` to the folder containing the file.
5. Run:

   ```powershell
   python sales_summary.py
   ```

**Expected output:**

```
Hello, Data World!
Average Sales: 252.0
```

## 3️⃣ Data Analysis in Jupyter Notebook

> 💡 **Pro tip:** do this inside a virtual environment. Full guide: [notes-virtual-env.md](notes-virtual-env.md).

1. Install the stack:

   ```powershell
   pip install jupyter pandas numpy matplotlib seaborn
   ```

2. `cd` to your project folder.
3. Launch:

   ```powershell
   jupyter notebook
   ```

4. In the browser: **New → Python 3 (ipykernel)**.
5. Rename it with `snake_case.ipynb`, e.g. `exploratory_data_analysis.ipynb`.
6. In the first cell:

   ```python
   import pandas as pd

   df = pd.DataFrame({
       "Product": ["Laptop", "Mouse", "Keyboard"],
       "Sales": [55000, 1200, 2500]
   })
   df.head()
   ```

7. Press `Shift` + `Enter` to run it. Your first DataFrame is alive. 🎉

## 🖥️ Bonus: Notebooks Inside VS Code

1. Install the **Python** and **Jupyter** extensions.
2. Create or open a `.ipynb` file.
3. Click **Select Kernel** (top right) and choose your project's Python or `venv`.

You get notebooks, terminal, and Git in one window.

## 🧯 Common Snags

| Problem | Fix |
|:--------|:----|
| `python` is not recognized | Reinstall Python with the PATH box ticked |
| `pip` is not recognized | Try `python -m pip --version` |
| `jupyter` is not recognized | Activate your venv, or run `python -m notebook` |
| `ModuleNotFoundError` | You're in the wrong environment; activate the right one and `pip install` again |

&nbsp;

*First Published Date: Aug 24, 2026*&emsp;
<br>
*Last Updated Date: Sep 30, 2026*&emsp;
