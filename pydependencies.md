---
marp: true
author: Ian Lanham
theme: gaia
class: invert
paginate: true
math: mathjax
---

<style>
    h1 {
        font-family: Gill Sans;
        font-weight: 300;
    },
    body {
        font-family: IBM Plex Sans;
    }
</style>

# **Managing Python Dependencies for Data Science Projects**

Ian Lanham
Blog: [https://ianlanham.com](https://ianlanham.com)
GitHub: [https://github.com/ilanham](https://github.com/ilanham)
LinkedIn: [https://www.linkedin.com/in/ian-lanham/](https://www.linkedin.com/in/ian-lanham/)

---

# About Me

I've been a data professional for 10 years, starting as a DBA on SQL Server and PostgreSQL. In 2023, I earned my Master's Degree in Data Analytics from UCF. It opened my eyes about how data science and its use can impact decision making across different business sectors.  

I got hooked on Python in 2017, and haven't stopped talking about it since.  

---

# Survey

- Who uses Python regularly?
- How many people use Jupyter Notebook/Lab?
- How many people use Anaconda?
- How many people know about `pip`?
- How many people create virtual environments for their Python projects?

---

# Defining the Problem

- When working with new Python code, people typically do something like:
  - Install everything into the default Python environment ⚠️
  - With notebooks, install Jupyter standalone and create a virtual environment for everything else
  - Create a new virtual environment for _everything_ 😔
    - I do this, it's annoying
    - Jupyter gets duplicated in each virtual environment

<!---
# Adjust order here
- I want to touch on `pip` a little bit, then dive into Jupyter's dependencies
- From there, I'll focus advantages of `conda` and derivatives
- Then I can bring it back to "what if I want to develop Python code while also doing data science tasks" and highlight Chad Smith's web tool for exploring dependency management tools
--->

---

##### How are module dependencies handled in Python?

Since [PEP 621](https://peps.python.org/pep-0621/) they appear in the `pyproject.tml` file inside the root of the modules' repo

```toml
[build-system]
requires = [
    "setuptools",
...
    "numpy>=1.25",
    "scipy>=1.6.0",
]
```
- Taken from scikit-learn's `pyproject.toml` file
- Older style in `setup.py`

<!--- Talk about how each project on PyPI typically has a project structure like this.
Then get a dependency tree of a project like Jupyter's scope or PyTorch.
If no pyproject.toml, check setup.py.
--->

---

# pip

- Installs packages to our Python environment
- Typically step 1 of 99.99% of Python tutorials: `pip install <something>`
- Installs packages from the Python Package Index ([PyPI](https://pypi.org))

---

# venv

- Part of the Python standard library since 3.3, included after install from Python.org
- What is a virtual environment?
  - _"A folder structure that contains an isolated environment of Python and its dependencies"_
  - [YouTube - ArjanCodes - How to Create and Use Virtual Environments in Python With Poetry](https://youtu.be/0f3moPe_bhk?si=vQCP8VQrHx0rIR1d)
- tl;dr: for this topic, it isolates `pip` installs to a folder structure
- You can create a new `venv` and install different package versions from PyPI

<!--- Demo? --->

---

# virtualenv

- A project used prior to `venv`
- Much faster than `venv` when creating environments
- I can also specify a version of Python different than what I have installed:
  `virtualenv venv39 -p python3.9`

---

# Conda

- Comes with [Anaconda](https://www.anaconda.com), a distribution of Python geared towards scientific computing, data science, and machine learning
  - Can install non-Python libraries (C, R, Rust, Julia, etc.)
  - `conda install rust --channel conda-forge`
- More of a replacement for `pip` and PyPI, they manage their own versions of populay PyPI packages and ensure compatibility
- Default install is > 4 GB 👀, over 250 packages included

---

# Managing Sanity in your Conda Install

- Creates a default virtual environment `base`, activates **_any_** time you open a terminal
  - To turn it off: `conda config --set auto__activate_base false`
  - _You should do this if you have a Python install with your OS or you installed Python yourself from [python.org](https://python.org)_

---

# Anaconda Navigator

- Like a GUI for exploring packages installed into a Python virtual environment
- Very polished, and can be installed from conda forge using `mamba` too

<!--- Demo --->

---

# Miniconda and Mamba

- Mini-conda: The `conda` program without 3-4 GB of extra binaries
- `mamba`: `conda` written in C++ 🏎️
- [conda-forge](https://conda-forge.org): A community-driven alternative to base `conda` and the Anaconda channel

---

# Why not just use Anaconda-based options?

- Anaconda came before `pip` had a lot of the features and libraries it does now
  - 1.0 release was in 2012, comparable latest Python release was 3.2
- `pip` has matured greatly since the release of `conda`
- If you develop Python libraries (not just data science/scientific computing), you may need to use a different package management workflow

---

# Where does Jupyter fit into this?
- It has a **LOT** of dependencies
- Two separate products:
  1. Jupyter Notebook (older style, most common)
  2. JupyterLab
- Depending on how you use Jupyter (native, webhosted, VS Code plugin), you can run into lots of problems managing conflicting dependencies in the same notebook
- Conda (and conda-forge) handle the version control for us

---

# Flowchart for choosing dependency management

- Chart here to describe when we should go conda-based or pip-based workflows (or both)
<!--- This might need to go up front, where we talk about differences between the two approaches --->

---

# More pip-based Tools

---

# pipenv

- pipenv = pip + virtualenv + pyenv
  - https://youtu.be/jVcN49sHbBQ?si=HDH11U2GLV-LSxwt

---

# pip-tools

- Can be installed by `pipx`
- Comes with `pip-compile`, input requirements by `requirements.in`
- `pip-compile` creates a full requirements.txt file from a rougher "requirements.in" file
- Source: https://youtu.be/G8PApVvdkjQ?si=s5bGzrcM8ymzZkFd

---

# pipx

- It focuses on modules that can be called from the command line
- A great alternative to creating a separate virtual environment for *just one tool*
- The tools installed with `pipx` are available gloablly

---

# poetry

- A dependency and environment manager
- Also a build system
  - https://youtu.be/jVcN49sHbBQ?si=HDH11U2GLV-LSxwt
- It can also help you publish to PyPI

---

# Other Tools for dependency management
- Hatch
- Rye
- pyenv

---
