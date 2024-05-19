# oc20
## Status
- [x] Build bare-metal environment on top of `conda/2022-07-19` base environment (on Polaris)
- [ ] Test using Singularity container
  - [ ] Build Singularity container from provided `Dockerfile`
- [ ] Run to completion on Polaris

## Instructions
1. `module load conda/2022-07-19`
2. `conda activate base`
3. `conda activate /lus/grand/projects/datascience/foremans/polaris/miniconda3/envs/MLPerf-HPC-2022-07-19`
4. `cd /lus/grand/projects/datascience/foremans/projects/mlperf/2022/nvidia-optimized/optimized-hpc/oc20/pytorch`
5. `source configs/config_DGXA100_polaris.sh`
6. `NRANKS=$(wc -l < "${PBS_NODEFILE}")`
7. `NGPU_PER_RANK=$(nvidia-smi -L | wc -l)`
8. `NGPUS=$((${NRANKS}*${NGPU_PER_RANK}))`
9. Command:
  ```shell
    mpiexec --verbose --envall \
        -n "${NGPUS}" \
        --ppn "${NGPU_PER_RANK}" \
        --hostfile "${PBS_NODEFILE}" \
        ./bind_polaris.sh \
            python3 main.py \
            --batch_size 64 \
            --eval_batch_size 64 \
            --lr_initial=0.001 \
            --run_dir=outputs \
            --data /lus/grand/projects/datascience/MLPerf-datasets/oc20 \
            --amp \
            --num_workers="${NGPUS}"
  ```
  exits with:
  ```python
    OSError: [Errno 28] No space left on device: '/lus/grand/projects/datascience/MlPerf-datasets/oc20/oc20_data/s2ef/2M/train/data.0060.lmdb' -> '/dev/shm/oc20_data/s2ef/2M/train/data.0060.lmdb'
  Traceback (most recent call last):
    ...
  ```
  
