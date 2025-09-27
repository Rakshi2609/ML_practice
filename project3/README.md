# Project 3 – Linear Regression Practice

Focus: Predicting student scores from study hours and related small tabular datasets.

## Key Notebook
- `test.ipynb`: Stable end-to-end example (load cleaned CSV, fit `LinearRegression`, evaluate metrics, make a sample prediction).

## Data Files
| File | Purpose |
|------|---------|
| `score.csv` | Original raw / malformed header example |
| `score_fixed.csv` | Clean synthesized dataset used for modeling |
| `score1.csv` | Intermediate variation |
| `student_data.csv`, `student_data_final.csv` | Experiments with student performance data |

## Typical Usage
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r project1/requirements.txt  # reuse base deps
pip install jupyter  # if needed
jupyter notebook project3/test.ipynb
```

## Model Snippet
```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn import metrics
import numpy as np

df = pd.read_csv('score_fixed.csv')
X = df[['Hours']]
y = df['Score']
model = LinearRegression().fit(X, y)
print('RMSE:', (metrics.mean_squared_error(y, model.predict(X)) ** 0.5))
print('Predict 6 hours:', model.predict([[6]])[0])
```

## Troubleshooting
| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| "Hours" column missing | Corrupt or merged header | Inspect `pd.read_csv(...).columns` and regenerate clean CSV |
| Notebook cell hangs | `input()` waiting for user | Replace with predefined variable |

## Next Ideas
- Add train/test split and compare metrics
- Visualize residuals
- Try polynomial features or regularization (Ridge/Lasso)

See root `README.md` for repo-wide guidance.
