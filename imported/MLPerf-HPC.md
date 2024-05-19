## MLPerf-HPC Submission: 2022

## `oc20`
- **Crashed**:
  - qsub: job **320950**.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov completed
  - `x3109c0s13b0n0.hsn.cm.polaris.alcf.anl.gov: rank 0 died from signal 7 and dumped corex3109c0s13b0n0.hsn.cm.polaris.alcf.anl.gov: rank 3 died from signal 15`
### Polaris
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
  

---

```bash
python3 -m pip install -r requirements.txt
python3 -m pip install --no-cache-dir torch-scatter
```

- `python3 -m pip install lmdb`

## DeepCam
```dockerfile
#RUN cd /opt/pytorch/pytorch/third_party/cudnn_frontend && \
#RUN cd /opt/pytorch/pytorch && \
RUN cd /opt && git clone https://github.com/NVIDIA/apex.git && \
#RUN apt update -y && apt install -y liburcu-dev linux-headers-generic #linux-headers-$(uname -r)
#RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin && \
RUN pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/nightly --upgrade nvidia-dali-nightly-cuda110
RUN pip install h5py mpi4py
RUN pip install nvidia-pyindex && \
RUN sed -i '/apex.contrib.multihead_attn/d' /opt/conda/lib/python3.8/site-packages/nvidia_dlprof_pytorch_nvtx/nvmarker.py
RUN pip install wandb
RUN pip install "git+https://github.com/mlcommons/logging.git@hpc-1.0.0-rc1"
RUN cd /opt/io_helpers && python setup.py install
#RUN cd /opt && git clone https://github.com/rapidsai/kvikio && \
RUN cd /opt/deepCam && git init
RUN mkdir -p /data
```

