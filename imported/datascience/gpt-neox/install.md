# `gpt-neox`

- First, from within the `conda/2022-07-19` base environment:

  ```shell
  python3 -m venv venv --system-site-packages
  source venv/bin/activate
  python3 -m pip install -r requirements/requirements.txt
  ```

  gave the following error:
  ```txt
  Building wheels for collected packages: ftfy, mpi4py, jieba, openai, pycountry, sqlitedict, deepspeed, subprocess32, sacremoses
    Building wheel for ftfy (setup.py) ... done
    Created wheel for ftfy: filename=ftfy-6.0.1-py3-none-any.whl size=41572 sha256=1e2b76b050faffa8b334b7d1cf9a2dfceafe844c4924a6f623563512e2db75b4
    Stored in directory: /tmp/pip-ephem-wheel-cache-3t1pp5nl/wheels/ea/fd/82/b600967fbbe79767c7bfef97cd5f82bf26c4e6d96a98260d4d
    Building wheel for mpi4py (setup.py) ... error
    error: subprocess-exited-with-error
  
    × python setup.py bdist_wheel did not run successfully.
    │ exit code: 1
    ╰─> [84 lines of output]
    ...
          _configtest.c:2:10: fatal error: mpi.h: No such file or directory
            2 | #include <mpi.h>
              |          ^~~~~~~
        compilation terminated.
        error: Cannot compile MPI programs. Check your configuration!!!
        [end of output]
  
    note: This error originates from a subprocess, and is likely not a problem with pip.
    ERROR: Failed building wheel for mpi4py
  ```

- 1. Modify `requirements/requirements.txt` to:

``` git+https://github.com/EleutherAI/DeeperSpeed.git@eb7f5cff36678625d23db8a8fe78b4a93e5d2c75#egg=deepspeed
einops>=0.3.0
ftfy>=6.0.1
lm_dataformat>=0.0.20
lm_eval>=0.2.0
mpi4py
numpy
pybind11
regex
sentencepiece
six
tokenizers>=0.10.2
transformers~=4.16.0
wandb>=0.10.28
```

- Install requirements from modified `requirements.txt` file:
  - `python3 -m pip install -r requirements/requirements.txt`
- These installed successfully, but then trying to train I encountered the following error:

  ```
  x3109c0s13b1n0: helpers.cpp:21:10: fatal error: pybind11/numpy.h: No such file or directory
  x3109c0s13b1n0:    21 | #include <pybind11/numpy.h>
  x3109c0s13b1n0:       |          ^~~~~~~~~~~~~~~~~~
  x3109c0s13b1n0: compilation terminated.
  ```
  
  which I was able to resolve by:
  ```shell
  conda run python3 -m pip install "pybind11==2.6.2" "numpy==1.22.0"
   ```
   
- Create (modified) hostfile:
  - From the documentation:
  > If you need to supply a **hostfile** for use with the MPI-based DeepSpeed launcher, you can set the environment variable `DLTS_HOSTFILE` to point to the hostfile.

  ```shell
  $ cat $PBS_NODEFILE > hostfile
  $ sed -e 's/$/slots=4' -i hostfile
  $ export DLTS_HOSTFILE=hostfile
  ```

- Prepare Data
  ```shell
  python prepare_data.py -d ./data
  ```

- Train:
  ```shell
  python3 ./deepy.py train.py -d configs small.yml local_setup.yml`
  ```

