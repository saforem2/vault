# Issues
- From the [Developer Installation](https://deephyper.readthedocs.io/en/latest/install/thetagpu.html#developer-installation) for ThetaGPU:

> Follow the [Conda environment](https://deephyper.readthedocs.io/en/latest/install/thetagpu.html#thetagpu-conda-environment) installation and replace `pip install deephyper[analytics]` by:
>   `git clone -b develop https://github.com/deephyper/deephyper.git`
>   `pip install -e "deephyper[dev,analytics]"`
```
```
---
- Should be

`python3 -m pip install -e ".[dev,analytics,nas]"`