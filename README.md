# CAUSE: **C**ausality from **A**ttrib**U**tions on **S**equence of **E**vents

## Installation

### Prerequisites
- conda 23.11.0 or later
- `brew install swig`(for installing `tick` from source)

### 1. Create a new conda environment
```shell
conda create -n CAUSE python=3.8
conda activate CAUSE
````

### 2. Install `tick`
`tick` is a Python library for statistical learning, with a particular emphasis on time-dependent models, such as point processes, and tools for generalized linear models.
In this repository, we use `tick` to generate datasets from Hawkes processes.

Since `tick` is not available on `pip` for Apple silicon machines, we need to install it from source.

First, clone the `tick` repository:
```shell
git clone git@github.com:X-DataInitiative/tick.git
git checkout 5b8ef9d1b2ef46c89016e3aabae7071f1222c9ed
git submodule update --init
cd tick
```

Then, install the dependencies. `numpy` must be `1.22`, not later, to work with `tick` and this repository.
```shell
pip install numpy=1.22
pip install -r requirements.txt
```

Lastly, modify 207-209 lines of `setup.py` file:
```python
build_dir = "build/lib.{}-cpython-{}"+PYVER_DBG
build_dir = build_dir.format(distutils.util.get_platform(),
                             "".join(sys.version.split(".")[:2]))
```

And install:
```shell
python setup.py build install
```

Check if `tick` is installed correctly:
```shell
cd ..
python -c "import tick"
```

### 3. Install the remaining dependencies
```shell
conda env update --file environment.yml
```

## How to Run

Run the scripts for individual datasets
```
./scripts/run_excitation.sh all
./scripts/run_inhibition.sh all
./scripts/run_syngergy.sh all
./scripts/run_iptv.sh all
./scripts/run_memetracker.sh all
```

If you find this repo useful, please consider to cite:
```
@inproceedings{zhang2020cause,
  title={Cause: Learning granger causality from event sequences using attribution methods},
  author={Zhang, Wei and Panum, Thomas and Jha, Somesh and Chalasani, Prasad and Page, David},
  booktitle={International Conference on Machine Learning},
  pages={11235--11245},
  year={2020},
  organization={PMLR}
}
```