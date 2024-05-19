---
title: libaio
date created: Friday, December 2nd 2022, 2:49:55 pm
---
# DeepSpeed with `libaio`

> [!INFO] 
> The following instructions are for Polaris @ ALCF
> 
> Written: 2022-12-02 by Sam Foreman

## Install Instructions

```Shell
module load conda/2022-09-08-hvd-nccl
conda activate base
conda create \
    --clone base \
    --prefix "/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl" \
    --experimental-solver=libmamba
    
conda activate "/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl"

python3 -m pip install "triton==1.0.0"
mamba install -c conda-forge libaio

export LD_LIBRARY_PATH="${CONDA_PREFIX}/lib:${LD_LIBRARY_PATH}"

git clone https://github.com/microsoft/DeepSpeed
cd DeepSpeed
git pull

CFLAGS="-I${CONDA_PREFIX}/include/" LDFLAGS="-L${CONDA_PREFIX}/lib/" DS_BUILD_OPS=1 bash install.sh --verbose
```

# To Use

```bash
$ module load conda/2022-09-08-hvd-nccl
$ conda activate base
$ conda activate "/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl"
$ ds_report
--------------------------------------------------
DeepSpeed C++/CUDA extension op report
--------------------------------------------------
NOTE: Ops not installed will be just-in-time (JIT) compiled at
      runtime if needed. Op compatibility means that your system
      meet the required dependencies to JIT install the op.
--------------------------------------------------
JIT compiled ops requires ninja
ninja .................. [OKAY]
--------------------------------------------------
op name ................ installed .. compatible
--------------------------------------------------
cpu_adam ............... [YES] ...... [OKAY]
cpu_adagrad ............ [YES] ...... [OKAY]
fused_adam ............. [YES] ...... [OKAY]
fused_lamb ............. [YES] ...... [OKAY]
sparse_attn ............ [YES] ...... [OKAY]
transformer ............ [YES] ...... [OKAY]
stochastic_transformer . [YES] ...... [OKAY]
async_io ............... [YES] ...... [OKAY]
utils .................. [YES] ...... [OKAY]
quantizer .............. [YES] ...... [OKAY]
transformer_inference .. [YES] ...... [OKAY]
spatial_inference ...... [YES] ...... [OKAY]
--------------------------------------------------
DeepSpeed general environment info:
torch install path ............... ['/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib/python3.8/site-packages/torch']
torch version .................... 1.12.0a0+git664058f
torch cuda version ............... 11.6
torch hip version ................ None
nvcc version ..................... 11.6
deepspeed install path ........... ['/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib/python3.8/site-packages/deepspeed']
deepspeed info ................... 0.7.7+bbe030c5, bbe030c5, master
deepspeed wheel compiled w. ...... torch 1.12, cuda 11.6
4.12s user 10.42s system 388% cpu 3.749s total
```


## Benchmarks

### All Reduce

> [!done]- "ALL REDUCE"
> - `deepspeed --hostfile=hostfile all_reduce.py`
> ```Shell
> $ deepspeed --hostfile=hostfile all_reduce.py
> /bin/sh: /lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib/libtinfo.so.6: no version information available (required by /lib64/libreadline.so.7)
> [2022-12-02 21:47:12,197] [INFO] [runner.py:417:main] Using IP address of 10.201.4.132 for node x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov
> [2022-12-02 21:47:12,200] [INFO] [multinode_runner.py:65:get_cmd] Running on the following workers: x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov,x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov
> [2022-12-02 21:47:12,200] [INFO] [runner.py:508:main] cmd = pdsh -S -f 1024 -w x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov,x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov export PYTHONUSERBASE=/home/foremans/.local/polaris/conda/2022-09-08-hvd-nccl; export PYTHONPATH=/lus/grand/projects/datascience/foremans/locations/polaris/projects/DeepSpeed/benchmarks/communication; export PATH=/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/bin:/soft/datascience/conda/2022-09-08-hvd-nccl/mconda3/condabin:/soft/compilers/cudatoolkit/cuda-11.6.2/bin:/soft/libraries/nccl/nccl_2.14.3-1+cuda11.6_x86_64/include:/opt/cray/pe/pals/1.1.7/bin:/opt/cray/pe/craype/2.7.15/bin:/opt/cray/pe/gcc/11.2.0/bin:/home/foremans/.linuxbrew/opt/glibc/sbin:/home/foremans/.linuxbrew/opt/glibc/bin:/run/user/33638/fnm_multishells/60741_1670013571280/bin:/run/user/33638/fnm_multishells/60737_1670013571252/bin:/home/foremans/.fnm:/opt/cray/pe/perftools/22.05.0/bin:/opt/cray/pe/papi/6.0.0.14/bin:/opt/cray/libfabric/1.11.0.4.125/bin:/opt/clmgr/sbin:/opt/clmgr/bin:/opt/sgi/sbin:/opt/sgi/bin:/home/foremans/bin:/usr/local/bin:/usr/bin:/bin:/opt/c3/bin:/usr/lib/mit/bin:/usr/lib/mit/sbin:/opt/pbs/bin:/sbin:/home/foremans/.linuxbrew/bin:/home/foremans/.linuxbrew/sbin:/home/foremans/.cargo/bin:/home/foremans/.local/bin:/home/foremans/.fzf/bin:/opt/cray/pe/bin; export LD_LIBRARY_PATH=/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib:/soft/compilers/cudatoolkit/cuda-11.6.2/extras/CUPTI/lib64:/soft/compilers/cudatoolkit/cuda-11.6.2/lib64:/soft/libraries/trt/TensorRT-8.4.3.1.Linux.x86_64-gnu.cuda-11.6.cudnn8.4/lib:/soft/libraries/nccl/nccl_2.14.3-1+cuda11.6_x86_64/lib:/soft/libraries/cudnn/cudnn-11.6-linux-x64-v8.4.1.50/lib:/opt/cray/pe/gcc/11.2.0/snos/lib64:/opt/cray/pe/papi/6.0.0.14/lib64:/opt/cray/libfabric/1.11.0.4.125/lib64; export https_proxy=http://proxy.alcf.anl.gov:3128; export http_proxy=http://proxy.alcf.anl.gov:3128; export CFLAGS=-I/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/include/; export LDFLAGS=-L/lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib/;  cd /lus/grand/projects/datascience/foremans/locations/polaris/projects/DeepSpeed/benchmarks/communication; /lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/bin/python -u -m deepspeed.launcher.launch --world_info=eyJ4MzIxMWMwczM3YjBuMC5oc24uY20ucG9sYXJpcy5hbGNmLmFubC5nb3YiOiBbMCwgMSwgMiwgM10sICJ4MzIxMWMwczM3YjFuMC5oc24uY20ucG9sYXJpcy5hbGNmLmFubC5nb3YiOiBbMCwgMSwgMiwgM119 --node_rank=%n --master_addr=10.201.4.132 --master_port=29500 all_reduce.py pdsh: /lus/grand/projects/datascience/foremans/locations/polaris/miniconda3/envs/2022-09-08-hvd-nccl/lib/libtinfo.so.6: no version information available (required by /lib64/libreadline.so.7) x3211c0s37b1n0: Warning: Permanently added 'x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov' (ECDSA) to the list of known hosts.
> x3211c0s37b0n0: [2022-12-02 21:47:16,624] [INFO] [launch.py:142:main] WORLD INFO DICT: {'x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3], 'x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3]}
> x3211c0s37b0n0: [2022-12-02 21:47:16,624] [INFO] [launch.py:148:main] nnodes=2, num_local_procs=4, node_rank=0
> x3211c0s37b0n0: [2022-12-02 21:47:16,624] [INFO] [launch.py:161:main] global_rank_mapping=defaultdict(<class 'list'>, {'x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3], 'x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov': [4, 5, 6, 7]})
> x3211c0s37b0n0: [2022-12-02 21:47:16,624] [INFO] [launch.py:162:main] dist_world_size=8
> x3211c0s37b0n0: [2022-12-02 21:47:16,624] [INFO] [launch.py:164:main] Setting CUDA_VISIBLE_DEVICES=0,1,2,3
> x3211c0s37b0n0: [2022-12-02 21:47:22,735] [INFO] [comm.py:633:init_distributed] Initializing TorchBackend in DeepSpeed with backend nccl
> x3211c0s37b1n0: [2022-12-02 21:48:10,503] [INFO] [launch.py:142:main] WORLD INFO DICT: {'x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3], 'x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3]}
> x3211c0s37b1n0: [2022-12-02 21:48:10,503] [INFO] [launch.py:148:main] nnodes=2, num_local_procs=4, node_rank=1
> x3211c0s37b1n0: [2022-12-02 21:48:10,503] [INFO] [launch.py:161:main] global_rank_mapping=defaultdict(<class 'list'>, {'x3211c0s37b0n0.hsn.cm.polaris.alcf.anl.gov': [0, 1, 2, 3], 'x3211c0s37b1n0.hsn.cm.polaris.alcf.anl.gov': [4, 5, 6, 7]})
> x3211c0s37b1n0: [2022-12-02 21:48:10,503] [INFO] [launch.py:162:main] dist_world_size=8
> x3211c0s37b1n0: [2022-12-02 21:48:10,503] [INFO] [launch.py:164:main] Setting CUDA_VISIBLE_DEVICES=0,1,2,3
> x3211c0s37b0n0:
> x3211c0s37b0n0: ---- Performance of all_reduce on 8 devices ---------------------------------------------------------
> x3211c0s37b0n0: Size (Bytes)         Description               Duration             Throughput (Gbps)    BusBW (Gbps)
> x3211c0s37b0n0: ----------------------------------------------------------------------------------------------------
> x3211c0s37b0n0: 31.67 GB             8501054668x4              3176.620 ms          171.272              149.863
> x3211c0s37b1n0: [2022-12-02 21:51:21,719] [INFO] [launch.py:350:main] Process 57911 exits successfully.
> x3211c0s37b1n0: [2022-12-02 21:51:21,719] [INFO] [launch.py:350:main] Process 57910 exits successfully.
> x3211c0s37b1n0: [2022-12-02 21:51:21,719] [INFO] [launch.py:350:main] Process 57909 exits successfully.
> x3211c0s37b1n0: [2022-12-02 21:51:21,719] [INFO] [launch.py:350:main] Process 57912 exits successfully.
> x3211c0s37b0n0: [2022-12-02 21:51:32,214] [INFO] [launch.py:350:main] Process 16309 exits successfully.
> x3211c0s37b0n0: [2022-12-02 21:51:32,215] [INFO] [launch.py:350:main] Process 16308 exits successfully.
> x3211c0s37b0n0: [2022-12-02 21:51:32,215] [INFO] [launch.py:350:main] Process 16311 exits successfully.
> x3211c0s37b0n0: [2022-12-02 21:51:32,215] [INFO] [launch.py:350:main] Process 16310 exits successfully.
> 4.03s user 10.23s system 5% cpu 4:24.48s total
> ```

