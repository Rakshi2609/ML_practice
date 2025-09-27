# ML Practice Workspace

A lightweight collection of small machine learning practice notebooks and datasets. The repository is intentionally simple so you can experiment quickly without heavyweight frameworks.

## Repository Structure

```
.
├── project1/            # Basic data exploration & sorting notebook (e.g., `sort.ipynb`)
│   ├── requirements.txt # Minimal dependency list for classic ML stack
│   └── venv/            # (Local virtual environment – ignored by Git after cleanup)
├── project3/            # Linear Regression & student score prediction experiments
│   ├── test.ipynb       # Main working notebook with cleaned regression example
│   ├── project1.ipynb   # Additional exploration / earlier experiments
│   ├── score*.csv       # Raw / intermediate score datasets
│   └── student_*.csv    # Student performance related datasets (cleaning attempts)
└── README.md            # You are here
```

## Goals
- Practice Python data wrangling (Pandas)
- Implement simple regression models (scikit-learn LinearRegression)
- Learn good reproducible workflow habits (virtual env, requirements, .gitignore)
- Safely version notebooks and data without committing virtual environments

## Getting Started

### 1. Create & Activate a Virtual Environment (Recommended)
On Windows PowerShell:
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```
(On CMD use: `.\.venv\Scripts\activate.bat`)

### 2. Upgrade pip (optional but recommended)
```powershell
python -m pip install --upgrade pip
```

### 3. Install Dependencies
You can either use the minimal per-project list or create a consolidated root one.
From `project1/`:
```powershell
pip install -r project1/requirements.txt
```
If you need Jupyter:
```powershell
pip install jupyter jupyterlab
```

### 4. Launch Jupyter
```powershell
jupyter notebook
```
(or `jupyter lab` if installed)

### 5. Open Notebooks
- `project3/test.ipynb` contains a working linear regression pipeline using a cleaned dataset (`score_fixed.csv`).
- Inspect the debug / data preparation cells to understand how malformed CSV headers were diagnosed and corrected.

## Data Notes
- `score.csv` and variants: Original & intermediate forms; some had header formatting issues (merged column names). `score_fixed.csv` is the clean synthesized version used for modeling.
- `student_data*.csv`: Experiments with cleaning, merging, or normalizing student-related features.
- Keep raw vs. derived datasets separated when possible; consider adding a `data/` folder with subfolders (`raw/`, `processed/`) as the project grows.

## Typical Linear Regression Flow (As Implemented)
```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn import metrics
import numpy as np

data = pd.read_csv("score_fixed.csv")
X = data[["Hours"]]
y = data["Score"]
model = LinearRegression().fit(X, y)

pred = model.predict([[6]])  # Example prediction
mse = metrics.mean_squared_error(y, model.predict(X))
rmse = np.sqrt(mse)
print(f"Prediction for 6 hours: {pred[0]:.2f}")
print(f"RMSE: {rmse:.4f}")
```

## Git Hygiene
Already handled / recommended:
- Added a comprehensive `.gitignore` to exclude: virtual environments (`venv/`, `.venv/`), `__pycache__/`, Jupyter checkpoints, build artifacts, OS clutter, and large ML artifacts.
- Removed previously committed `venv` folders from Git history index (they will not reappear if kept out of the working tree or remain ignored).

If you accidentally commit a venv again:
```powershell
git rm -r --cached venv .venv
```

## Freezing Dependencies
After installing everything you actually use:
```powershell
pip freeze > requirements.txt
```
(Consider placing a curated list under version control instead of the full freeze for cleanliness.)

## Suggested Enhancements (Next Steps)
- Add a root `requirements.txt` or `pyproject.toml`
- Separate data into `data/raw` and `data/processed`
- Introduce lightweight tests (e.g., `pytest`) to validate data assumptions
- Add a `LICENSE` file (MIT, Apache-2.0, etc.)
- Add a `Makefile` or simple PowerShell script for setup automation

## Contributing
Personal practice repo for now. If expanded, define style guidelines (PEP8), code formatting (black), and pre-commit hooks.

## License
Not yet specified. Add a LICENSE file before sharing publicly.

## Troubleshooting
| Issue | Cause | Fix |
|-------|-------|-----|
| Notebook cell "hangs" | Waiting on `input()` | Replace with predefined variables or widgets |
| Column not found error | Malformed CSV header | Inspect `df.columns`; recreate a clean CSV |
| Virtual env files staged | venv created before `.gitignore` | Run `git rm -r --cached venv .venv` |

---
Happy experimenting! Feel free to expand structure as your practice grows.
