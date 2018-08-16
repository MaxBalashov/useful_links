# Write less terrible code with Jupyter Notebook
Original article: https://blog.godatadriven.com/write-less-terrible-notebook-code

# Summary

## TL;DR

1. Move your code from your Notebook into a Python package.
2. Install the package in your virtual environment in development mode.
3. Use the `%autoreload` magic to automatically re-import updated code.

## 1. From Notebook to package

Follow to such structure:

```
example_project/
├── notebooks/          <-- Jupyter notebooks.
    └── Untitled4.ipynb
├── exampleproject/     <-- Python package with source code.
    └── __init__.py     <-- Make the folder a package.
    └── example.py      <-- Example module in the package.
└── setup.py            <-- Install and distribute your module.
```

## 2. Using your package in a Notebook

```bash
$ pwd
~/example_project
$ conda activate example_venv
(example_venv) $ pip install --editable .
running develop
...
Finished processing dependencies for cropyield==0.0.1
```

The `setup.py` contains instructions for `pip` to install the package in `example_venv`.
Option `--editable` allows you to edit your code without re-installing the package to get the changes.

Or use insted of "`$ pip...`" (check the [docs](https://pip.pypa.io/en/latest/reference/pip_install/#editable-installs)):
```bash
python setup.py develop --no-deps
```

## 3. The `%autoreload` magic

Add `%autoreload` at the top of your Notebook:

```python
# Load the extension
%load_ext autoreload
# Autoreload all modules
%autoreload 2
```