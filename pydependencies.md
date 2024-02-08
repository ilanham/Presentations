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
Blog: https://ianlanham.com
LinkedIn: https://www.linkedin.com/in/ian-lanham/

---

# About Me

I've been a data professional for 10 years, starting as a DBA on SQL Server and PostgreSQL. I earned my Master's in Data Analytics from UCF in 2023, and it opened my eyes about how Data Science and its use can impact decision making across numerous areas.  

I love learning more about the applications of data science. It can provide answers to the "So what?" question we sometimes run into with data collection and management.

---

# Survey

- Who uses Python regularly?
- How many people know how to use `pip`?
- How many people use Anaconda?
- How many people use Google Colab or something similar?

---

# Defining the Problem

When you're reading or practicing new code, how many of you create a new virtual environment, hatch, or install it by poetry? (too specific here but should be generalized)

---

# How are module dependencies handled in Python?

Since PEP###, they appear in the `pyproject.tml` file inside the root of a module you find on pypi.org

```toml
[build-system]
requires = [
    "setuptools",
    "wheel",
    "Cython>=0.29.33",
    "numpy>=1.25",
    "scipy>=1.6.0",
]
```
-- Taken from scikit-learn's `pyproject.toml` file

---

# pip

- A note about installing tools via `pipx`
  - It doesn't solve our immediate problem, but it lets us cleanly install tools that help with the symptoms

---

# venv

- Part of the Python standard library since 3.3, included after install from Python.org
- What is a virtual environment?
  - "A folder structure that contains an isolated environment of Python and its dependencies"
  - [YouTube - ArjanCodes - How to Create and Use Virtual Environments in Python With Poetry](https://youtu.be/0f3moPe_bhk?si=vQCP8VQrHx0rIR1d)

---

# virtualenv

- A project used prior to `venv`
- Much faster than `venv` when creating environments
- I can also specify a version of Python different than what I have installed:
  `virtualenv venv39 -p python3.9`

---

# Conda

- Comes with Anaconda, a distribution of Python geared towards scientific computing, data science, and machine learning
  - Can install non-Python libraries (C, R, Rust, Julia, etc.)
  - `conda install rust --channel conda-forge`
- More of a replacement for `pip` and PyPI, they manage their own versions that are cross-compatible
- Default install is > 4 GB 👀, over 250 packages included

---

## A note about Miniconda and Mamba

- Mini-conda: The `conda` program without 3-4 GB of extra binaries
- `mamba`: `conda` written in C++
- An excellent alternative to base `conda` and the Anaconda channel

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
