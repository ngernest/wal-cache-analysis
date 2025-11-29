# WAL Cache Analysis Methodology

This is a cache analysis library based on the methodology presented in our paper
"An Extensible and Flexible Methodology for Analyzing the Cache Performance of Hardware Designs".

## Setup

This project uses `uv` for Python environment management. 
(If you don't have `uv` installed, get it from [https://github.com/astral-sh/uv](https://github.com/astral-sh/uv).)

We create a virtual environment for Python 3.10 as follows:
```bash
$ uv venv wal_cache --python 3.10
$ source wal_cache/bin/activate
```

### Quick Start

1. Install Git LFS to fetch the waveforms:
```bash
$ brew install git-lfs
$ git lfs install
$ git lfs pull  # Downloads the actual FST trace files
```

2. Install dependencies:
```bash
uv pip install pylibfst git+https://github.com/ics-jku/wal.git@731d2ad
```

Note: `pylibfst` does not currently work on Windows.

3. Fix a known bug in `pylibfst` 0.2.1:

Open `wal_cache/lib/python3.10/site-packages/pylibfst/helpers.py` and add the following line after line 34 (after the `Signals = namedtuple...` line):
```python
signals = Signals(signals_by_name, signals_by_handle)
```

This fixes an `UnboundLocalError` that occurs when processing FST files without variables.

### Running the Examples

To analyze the exemplary IBEX waveforms:
```bash
wal ibex.wal traces/ibex_bubblesort_disabled.fst
```
or
```bash
wal ibex.wal traces/ibex_bubblesort_enabled.fst
```
