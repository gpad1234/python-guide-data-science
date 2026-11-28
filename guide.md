# New Session Guide

Use this guide whenever you begin working in this project. Run commands from the repository root:

```bash
cd /Users/gp/learning-datascience/python-guide
```

## 1. Start the virtual environment

Activate the existing `.venv`:

```bash
source .venv/bin/activate
```

The terminal prompt should begin with `(.venv)`. Verify that the terminal is using this project's Python:

```bash
which python
python --version
python -c "import numpy, pandas; print(numpy.__version__, pandas.__version__)"
```

The `which python` command should resolve to `.venv/bin/python`.

If `.venv` has not been created yet, create and configure it:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## 2. Open a notebook

Start JupyterLab with the virtual environment:

```bash
jupyter lab
```

Open one of the notebooks:

- `01_python_basics.ipynb`
- `02_numpy_pandas.ipynb`
- `03_visualization.ipynb`
- `04_first_ml_model.ipynb`

In VS Code:

1. Open the notebook.
2. Select the kernel named `.venv (3.13.11)`, or select `.venv/bin/python`.
3. Run cells from top to bottom.
4. Save the notebook after changes.

Do not start Jupyter without first activating `.venv`.

## 3. Verify the environment

Check that the core packages are available:

```bash
python -c "import jupyterlab, numpy, pandas, matplotlib, seaborn, sklearn"
```

Or run one notebook directly from the terminal:

```bash
jupyter nbconvert --to notebook --execute 02_numpy_pandas.ipynb \
  --output 02_numpy_pandas.ipynb \
  --ExecutePreprocessor.timeout=120
```

## 4. Install a missing package

Always install packages into `.venv`, not with the system Python:

```bash
python -m pip install package-name
python -m pip freeze
```

If the package belongs in this project, add it to `requirements.txt` and update the environment:

```bash
python -m pip install -r requirements.txt
```

## 5. Troubleshooting

### Notebook cannot import NumPy, pandas, or another package

The notebook is likely connected to the wrong kernel.

1. Select `.venv/bin/python` or `.venv (3.13.11)`.
2. Restart the kernel.
3. Run the following in a notebook cell:

   ```python
   import sys
   print(sys.executable)
   ```

   The output should contain `/Users/gp/learning-datascience/python-guide/.venv/`.

### Activation is missing or `.venv` is broken

Recreate the environment:

```bash
rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

This command is safe for this project because `.venv` is disposable and should not be committed.

### JupyterLab cannot start

With `.venv` activated, verify Jupyter:

```bash
which jupyter
jupyter --version
```

If Jupyter is missing, reinstall the requirements:

```bash
python -m pip install -r requirements.txt
```

## 6. End the session

Save notebook changes, stop JupyterLab with `Ctrl+C` in its terminal, and deactivate the environment:

```bash
deactivate
```

## 7. Reading notes for `04_first_ml_model.ipynb`

### First ML model: classification with scikit-learn

#### Example 3: Compare with logistic regression

A simpler linear model gives us a baseline to compare with the random forest.

#### Example 4: Tune a random forest with GridSearchCV

**Model settings**

A random forest combines many decision trees and uses their majority prediction (classification) or average prediction (regression). It is controlled by **hyperparameters**, which are settings chosen before training. Two important random forest hyperparameters are:

- `n_estimators`: the number of trees in the forest.
- `max_depth`: the maximum depth of each tree. A deeper tree can learn more detail, but it may overfit by memorizing the training data.

**Hyperparameter tuning**

Hyperparameter tuning searches for settings that perform well on unseen data. `GridSearchCV` tries every combination supplied in `param_grid`. Here it will test:

- 2 values for `n_estimators`: 50 or 100
- 3 values for `max_depth`: `None`, 5, or 10
- 6 combinations in total

The `clf__` prefix means that the setting belongs to the pipeline step named `clf`, not to the preprocessing step.

**Cross-validation**

For every combination, 5-fold cross-validation divides the training data into 5 parts. The model trains on 4 parts and validates on the remaining part. This repeats 5 times, so 30 model fits are performed (6 combinations x 5 folds). The combination with the highest mean validation accuracy becomes the best model.

`search.fit(...)` automatically retrains the best combination on the complete training set. `search.best_estimator_` is therefore ready to evaluate on the test set.

Finally, measure the selected model on data it did not use during tuning.

#### Exercises

1. Which model is easier to interpret: logistic regression or random forest?
2. Add features (family size, title) and measure the change.
3. Print the test-set classification report for `search.best_estimator_`.
