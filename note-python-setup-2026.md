- Operating System (OS): Windows
- Python Version: v3.12+
- Code Editor: Visual Studio Code (VS Code)
- Interactive Environment: Jupyter Notebook

# Steps to Install Python on Windows:
1. Go to [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/).
2. Download the latest Windows Installer (`.exe` 64-bit).
3. Run the downloaded `.exe` file.
4. **Important:** Check the box that says **"Add python.exe to PATH"** at the bottom of the installer window.
5. Click "Install Now".
6. Wait for the setup progress bar to finish, then click "Close".

To check if Python and `pip` have successfully been installed, open Command Prompt or PowerShell and type:
```powershell
python --version
pip --version
```

# Steps to Write and Run a Simple Python Program in a Text Editor / CLI:
1. Open a text editor (e.g., VS Code or Notepad++).
2. Copy and paste the following code into the file:
```python
# Simple Python program for quick data summary
data = [120, 250, 310, 180, 400]
average_sales = sum(data) / len(data)

print("Hello, Data World!")
print(f"Average Sales: {average_sales}")
```
3. Save it as `sales_summary.py` (using `snake_case.py` naming convention).
4. Open Command Prompt or PowerShell.
5. Use the `cd` command to navigate to the folder where `sales_summary.py` is saved.
6. Type `python sales_summary.py` and press [ENTER] to run the script.

# Steps to Run Data Analysis in Jupyter Notebook:
1. Open Command Prompt or PowerShell.
2. Install Jupyter Notebook and core analytics libraries by running:
```powershell
pip install jupyter pandas numpy matplotlib seaborn
```
3. Navigate to your project directory using `cd`.
4. Launch Jupyter Notebook by typing:
```powershell
jupyter notebook
```
5. In the browser window that opens, click "New" >> "Python 3 (ipykernel)".
6. Rename the notebook using `snake_case.ipynb` (e.g., `exploratory_data_analysis.ipynb`).
7. Enter the following code into the first cell:
```python
import pandas as pd

df = pd.DataFrame({
    "Product": ["Laptop", "Mouse", "Keyboard"],
    "Sales": [55000, 1200, 2500]
})
df.head()
```
8. Press `Shift` + `Enter` to execute the cell and view the DataFrame output.

&nbsp;

*First Published Date: Aug 24, 2026*&emsp;
<br>
*Last Updated Date: Sep 29, 2026*&emsp;
