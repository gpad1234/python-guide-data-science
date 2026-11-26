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
