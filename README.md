# Python for Machine Learning: Learning Guide

Level: beginner · Goal: machine learning · Time: 10+ hrs/week (~16 weeks)

For complete environment startup and troubleshooting steps, see [guide.md](guide.md).

## Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

## Roadmap
| Weeks | Topic | Notebook | Outcome |
|---|---|---|---|
| 1-2 | Python fundamentals | `01_python_basics.ipynb` | Functions, loops, lists/dicts, files |
| 3-4 | NumPy and pandas | `02_numpy_pandas.ipynb` | Load, clean, group, and join data |
| 5-6 | Visualization and EDA | `03_visualization.ipynb` | Explore a dataset with matplotlib/seaborn |
| 7-8 | Stats and probability | (Khan Academy / StatQuest) | Distributions, hypothesis tests, correlation |
| 9-12 | ML with scikit-learn | `04_first_ml_model.ipynb` | Train/test split, regression, classification, cross-validation, metrics |
| 13-14 | Feature engineering, pipelines, tuning | build on notebook 04 | Reusable `Pipeline`, `GridSearchCV` |
| 15-16 | Capstone project | your own | End-to-end project on a Kaggle/UCI dataset, published on GitHub |
| After | Deep learning | PyTorch tutorials | Neural nets |

## Weekly rhythm (10 hrs)
- 4 hrs: study/tutorial
- 4 hrs: hands-on exercises
- 2 hrs: mini-project or review

## Resources
- Python: *Automate the Boring Stuff* (free online), CS50P
- Data: *Python for Data Analysis* (Wes McKinney, free online)
- ML: Andrew Ng's Machine Learning Specialization, *Hands-On ML* (Géron), scikit-learn docs
- Practice: Kaggle Learn, Kaggle Titanic and House Prices competitions

## Tips
- Code along; don't just read.
- Finish a small project every 2-3 weeks.
- Always evaluate on held-out data.
