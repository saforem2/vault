# Scaling Status @ ALCF

## Polaris

### `conda/2022-07-19`

- Setup:
  ```Shell
  $ # directly from a compute node, on Polaris
  $ module load conda/2022-07-19
  $ conda activate base
  $ cd /lus/eagle/projects/datascience/tensorflow-test
  ```

- [x] # GPUS: 1
  ```Shell
  CUDA_VISIBLE_DEVICES=0 python3 func.py
  ```

- [a] # GPUS: 2
  ```Shell
  $ CUDA_VISIBLE_DEVICES="0,1" mpiexec \
      -n 2 \
      --envall \
      --label \
      --verbose
    ```

- [f] # GPUS: 3
  ```Shell
  $ CUDA_VISIBLE_DEVICES="0,1,2" mpiexec \
      -n 3 \
      --envall \
      --label \
      --verbose
  ```
- [f] # GPUS: 4
  ```Shell
  $ CUDA_VISIBLE_DEVICES="0,1,2,3" mpiexec \
      -n 4 \
      --envall \
      --label \
      --verbose
  ```

