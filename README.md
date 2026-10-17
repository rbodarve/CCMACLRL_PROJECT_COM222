# Introduction to Machine Learning - Final Project

The final project for Introduction to Machine Learning subject.

---

## Table of Contents

- [Setup Instructions](#setup-instructions)
  - [Dependencies Installation](#dependencies-installation)
    - [Using Anaconda or Miniconda (Environment)](#using-anaconda-or-miniconda-environment)
    - [Using Python (Standalone)](#using-python-standalone)
  - [.env File](#env-file)
- [Running the Program](#running-the-program)
- [License](#license)
- [Contributors](#contributors)

---

## Setup Instructions

Below are the steps on how to run the code in your local machine. This will
assume that you already have Python or Anaconda in your machine.

### Dependencies Installation

The project has several dependencies that are needed. To install these
dependencies, just follow one of the items below.

#### Using Anaconda or Miniconda (Environment)

If you are using Anaconda or Miniconda, you can open to the directory using
terminal. If Python is able to run in your terminal, then you could use the
following command:

```bat
conda install --f "requirements.txt"
```

#### Using Python (Standalone)

Using a standalone python without environments such as Miniconda or Anaconda,
you could simply use the `pip` command in your terminal.

```bat
pip install -r "requirements.txt"
```

### .env File

The project comes with a file named `.env.example`, which serves as a template
for a `.env` file or `environment` file. The `.env` file contains all the
secret tokens that will be used by the program during runtime.

To set one up, you just have to copy the `.env.example` file and rename that
copy to `.env` file.

Open the file and provide the two tokens. These tokens are spotify's developer
API tokens which grants developers to use their web API for free.

**You can see yours in:**\
`Dashboard` → `<project_name>` → `Settings`

**Or basically, in a url similar to this:**\
`https://developer.spotify.com/dashboard/<project_id>/settings`

## Running the Program

Running the program is as simple as pressing a button (assuming you already have
Jupyter installed). If Jupyter is not yet installed, either install a VSCode
extension or install [Jupyter Notebook](https://jupyter.org/) into your local
machine.

When running the program, just press the `Run All` button or manually run every
cell from the top until the bottom.

## License

This project uses and is distributed under the [Unlicensed License](https://unlicense.org)
and is subject to all its terms and conditions.

See `LICENSE` for more information.

## Contributors

[![Contributors](https://contrib.rocks/image?repo=Virus5600/CCMACLRL_FINAL_PROJECT_COM222ML)](https://github.com/Virus5600/CCMACLRL_FINAL_PROJECT_COM222ML/graphs/contributors)

## Review notes (2026-10-17)

Run check 2026-10-17: main.ipynb runs top to bottom on Python 3.12 (~15 min, API cells stubbed); main-alt.ipynb fails only at its last cell.

1. **Environment.** The notebooks need Python ≥ 3.12 because they nest the same quotes inside f-strings; on 3.10 they fail at cell 6. Unzip `datapack/custom-2/dataset.csv.zip` before running (read in cell 89). `requirements.txt` lacks scikit-learn, requests and jupyter, lists `imblearn` although it is never imported, and `conda install --f` is not a valid flag: use `pip install -r requirements.txt`.
2. **Scaling.** Test sets are scaled by a new `StandardScaler` fitted on the test set itself (main cells 102, 129), not by the training scaler. Prediction songs are rescaled among themselves with both a `StandardScaler` and a `MinMaxScaler` (cell 73), and cell 78 scores the MinMax data. Reported test metrics are therefore not comparable with training.
3. **Labels.** RMSE is printed as "Mean Squared Error" and R² as "Accuracy %" (e.g. cell 79). Cell 144 prints `mse["nu"]` on the su and mu lines.
4. **Only the default config works.** `undersampling` ≠ `"test"` hits an undefined `key` (main cells 111, 138), and in main-alt `undersample(title=None)` raises `TypeError`. `saveInput=True` reloads unscaled data that still contains `track_popularity` (cells 105/107).
5. **main-alt.** The last cell (162) writes to `output/metrics/`, which does not exist (`OSError`), and ignores `saveOutput`. The cell 31 summary labels swap Singular and Multiple.
6. **Reproducibility.** No `random_state` is set, and the hold-out is 1% (main) / 0.1% (alt). The Spotify API cells (main 73/74) were not run; Spotify closed audio-features to new apps in Nov 2024, so they may fail with a new key.
