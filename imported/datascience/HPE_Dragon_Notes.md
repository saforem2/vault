---
title: HPE Dragon
date created: Monday, January 31st 2022, 6:41:26 pm
---
# HPE Dragon
---

# 2023-01-11

- [ ] Prepare material for Data Science meeting tomorrow

---

## Status (as of 2022-11-07)

> [!NOTE]+ Pete's email 2022-05-23
> Hi Sam,
> ...
>
> - `dragon-0.2`:
>     - mp.Pool now passes all but one mp unit test (remaining one is a minor issue that will be addressed later)
>     - mp.Queue is faster and more robust
>     - Improvements to Managed Memory to perform blocking allocations, when resources are under contention, and improved handling when allocations cannot be satisfied. This allows the aa_bench to run at full scale on a dual socket Rome box
>     - mp unit tests are now included in the package so customers can check them against Dragon
>     - A subset of Dragon unit tests are included in the package to installs can be verified (more tests will be added later)
>     - Dragon-native API examples are included in the package so customers can start to see how Dragon can be used directly
>     - Many minor bug fixes and improvements
>
> _This will be our last pre-release ahead of our first multi-node enabled pre-release._
>
> We are on track right now for that to become available in the July-August timeframe.
>
> This release is interesting enough now with Pool working well that common applications may scale better or get better performance, in particular if they were communication bound.
> A good example of this is examples/multiprocessing/numpy-mpi4py-examples/scipy_scale_work.py, which is adapted from a Toward Data Science article comparing Ray and multiprocessing.
>
> Dragon-backed multiprocessing achieves ~3X better performance for large image sizes due to much more efficient communication.
>
>...
>
> Cheers,
> Pete

# Take Aways
- Dragon is a modular runtime that makes distributed system programming much easier to do with great performance
    - Especially on HPC systems
    - Portability from laptop to HPC systems with little-to-no changes in code using `Dragon`
    - <mark class="blue">Will have an open-source implementation</mark>
- Implementing standard Python `multiprocessing` API over Dragon
    - Widely used and _standard_ Python API for parallel programming
    - Demonstrates Dragon's capability and feeds us requirements
- Many things can be implemented over Dragon
    - Parallel programming APIs for other languages
    - Tools, libraries, and applications
    - Entire workflows of serial and distributed applications
- Anything implemented over Dragon benefits from
    - Simpler to implement
    - Common and interoperable foundation
    - Consistent performance and scalability
---

# `dragon-0.2`
## Dragon

> Dragon is a distributed environment for developing high-performance tools, libraries, and applications at scale. This distribution package provides the necessary components to run the Python multiprocessing library using the Dragon implementation which provides greater scaling performance improvements over the legacy multiprocessing that is currently distributed with Python.

## Install
- Requires `python >= 3.9` to be on `$PATH`
- `tar -xvf dragon-0.2-b9aecd8f.tar.gz`
- `python3 -m pip install dragon-0.2-cp39-cp39-linux_x86_64.whl`
- `module use [/path to dragon-0.2]/modulefiles`
- `module load dragon`
- `bin`: The module file will set up access to the dragon command found in the `bin/` directory
- `examples`: Provides demonstration problems that provide some working examples of using multiprocessing with Dragon and of the Dragon API itself.
    - Also contains standard Python multiprocessing unit tests packaged for easier use with Dragon.
    - Contains `README.md` with additional information on examples
- `lib`: The lib directory contains the library files providing the underlying services needed by the Dragon implementation of multiprocessing in the `pip` installed wheel package.
    - The module command given above sets up a `$DRAGON_BASE_DIR` environment variable so these shared libraries can be found by the run-time when running Dragon multiprocessing programs.
- `dragon_unittests`: This directory contains a selection of Dragon-specific unit tests used in the development process. The tests are included as validation of a Dragon install.

## Running
1. Import Dragon and set dragon as the start method (similar to starting method for `spawn` or `fork`):
    ```python
    import dragon
    import multiprocessing as mp
    ...
    if __name__ == '__main__':
        # set the start method prior to using any multiprocessing methods
        mp.set_start_method('dragon')
        ...
    ```

    This must be done once for each application.

    Dragon is an API level replacement for multiprocessing, so to learn more about Dragon and what it can do, read up on [multiprocessing](https://docs.python.org/3/library/multiprocessing.html).

2. You must start your program using the `dragon` command. This not only starts your program, but it also starts the Dragon run-time services that provide the necessary infrastructure for running multiprocessing at scale.
    ```bash
    $ dragon myprog.py
    ```

    If you find that there are directions that would be helpful and are missing from our documentation, please make note and provide feedback.

## Environment Variables
- `$DRAGON_BASE_DIR`: Set by `dragon` module file, the base directory of the package
- `$DRAGON_DEBUG`: Set to any non-empty string to enable verbose logging
- `$_DRAGON_DEFAULT_SEG_SZ`: Set to the number of bytes for the default Managed Memory Pool

## Log Files
This pre-alpha release of Dragon will produce a log file for every execution of `dragon`. These are helpful when encountering an issue.

## Requirements
- `python >= 3.9` (e.g. `module load cray-python`)
- `GCC >= 9`

## Known Issues
If you want to use Dragon with an Anaconda distribution of Python, there will be `libstdc++` ABI incompatibilities.

A workaround is to move/rename `anaconda/lib/libstdc++.so*` to a subdirectory or other name. The desired version of `libstdc++.so` should come from `GCC 9` or later.

Dragon Managed Memory, a low-level component of the Dragon runtime, uses shared memory.

It is possible with this pre-alpha release that things go wrong while the runtime is coming down and files are left in `dev/shm`. It is good to check if files are left there if the runtime is killed or forced down without a clean exit. If multiprocessing features are used that are not yet fully supported, such as Pool, it is possible for Python processes to be left behind after the runtime exits.

Python multiprocessing applications that switch between start methods may fail with this due to how Queue is being patched in.

**Note**: To enable module commands on local Linux VM, add the following line to `~/.zshrc` or `~/.bashrc`:

```Shell
$ source /usr/share/modules/init/bash
```


![Dragon_ANL_102621](../../../../PDFs/Dragon_ANL_102621.pdf)

