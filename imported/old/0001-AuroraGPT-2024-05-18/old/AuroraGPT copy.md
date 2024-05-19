---
id: AuroraGPT
aliases:
  - Aurora GPT
tags: []
---

# Aurora GPT
---

## 2024-05

### 2024-05-17

> [!bug]- Sunspot`frameworks` comparison on `flash-attn`
>
> ![loss/lm-loss-annotated](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/ScreenShot-2024-05-18-010434@2x.png)
> ![loss-learning-rate](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/ScreenShot-2024-05-18-011714@2x.png)

> [!question]- \[TLDR\] Running Theory...
> TLDR and not complete / just my thoughts:
> there are two things going on:
> 
> 1. some underlying bug in the `flash-attn` implementation of `ipex`
> 
> - some underlying bug in the `flash-attn` implementation in `ipex`:
> 	- everything works correctly in the previous `frameworks/2023.12.15.001`
>         - since it only provides: {`pytorch` + `ipex`} , I then:
>             - installed {`intel-extension-for-deepspeed`, `DeepSpeed`} using the
>             instructions from the **new release** (this week) from Jerome
>             (`deepspeed==0.14.3`)
>             
> flash, no-flash both give identical losses independent of {LR, LR_WARMUP_FRAC, LR_DECAY_ITERS} 
> 
> ```bash
> for the module load frameworks/2023.12.15.001:
> DeepSpeed general environment info:
> torch install path ............... ['/opt/aurora/23.275.2/frameworks/aurora_nre_models_frameworks-2024.0/lib/python3.9/site-packages/torch']
> torch version .................... 2.1.0a0+cxx11.abi
> deepspeed install path ........... ['/lus/gila/projects/Aurora_deployment/foremans/projects/argonne-lcf/Megatron-DeepSpeed/deps/DeepSpeed/deepspeed']
> deepspeed info ................... 0.14.3+6b45e931, 6b45e931, yizhou/kernel_path
> deepspeed wheel compiled w. ...... torch 2.1
> shared memory (/dev/shm) size .... 503.15 GB
> ```

### 2024-05-16

#### Polaris

- [x] Working @ 12 Nodes with full Dolma v1.7 dataset
    - W&B Run: [stoic-dragon-1870](https://wandb.ai/aurora_gpt/AuroraGPT/runs/kcqqooth?nw=nwuserforemans)
    - logfile: \[`/eagle/a/f/p/ar/Megatron-DeepSpeed/train_aGPT_7B.sh.o1938158`\]

#### Sunspot

- ==Fix for new frameworks release== ??
    - Looked at:
        - `module use /soft/preview-modulefiles/ ; module show 24.086.0/frameworks/2024.04.15.002`
    - Seems like following these `module ...` instructions, I'm able to run with my `conda` install from:
        - `anl_24_q2_release/run_setup.sh`

    ```bash title="anl_24_q2_release_fix.sh"
    
    # [11:04:06 PM] [foremans@x1921c2s0b0n0] /gila/A/fo/anl_24_q2_release  release/anl_2024.5 !4 ?3
    $ eval "$(~/miniconda3/bin/conda shell.zsh hook)"
    
    # [11:04:14 PM] [foremans@x1921c2s0b0n0] /gila/A/fo/anl_24_q2_release  release/anl_2024.5 !4 ?3 miniconda3 4s
    $ conda activate anl_24_q2_release

    # [11:09:05 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ python3 -c 'from mpi4py import MPI'
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
    ImportError: /home/foremans/miniconda3/envs/anl_24_q2_release/lib/python3.9/site-packages/mpi4py/MPI.cpython-39-x86_64-linux-gnu.so: undefined symbol: MPI_Message_c2f
    [1]    14554 exit 1     python3 -c 'from mpi4py import MPI'
    
    # [11:09:32 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module use /home/ftartagl/graphics-compute-runtime/modulefiles
    
    # [11:09:43 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module load graphics-compute-runtime/agama-ci-devel-803.29
         UMD: agama-ci-devel-803.29 successfully loaded:
         UMD: graphics-compute-runtime/agama-ci-devel-803.29
    
    # [11:10:08 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module load spack-pe-gcc/0.6.1-23.275.2
    
    # [11:10:14 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module load gcc/12.2.0
    
    # [11:10:26 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module use /soft/preview-modulefiles/24.086.0
    
    Due to MODULEPATH changes, the following have been reloaded:
      1) mpich-config/collective-tuning/1024
    
    
    # [11:10:34 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ module load oneapi/release/2024.04.15.001
    
    Due to MODULEPATH changes, the following have been reloaded:
      1) mpich-config/collective-tuning/1024
    
    The following have been reloaded with a version change:
      1) intel_compute_runtime/release/agama-devel-736.25 => intel_compute_runtime/release/775.20     2) mpich/icc-all-pmix-gpu/52.2 => mpich/icc-all-pmix-gpu/20231026     3) oneapi/eng-compiler/2023.12.15.002 => oneapi/release/2024.04.15.001
    
    
    # [11:10:49 PM] [foremans@x1921c2s0b0n0] ~ anl_24_q2_release
    $ python3 -c 'from mpi4py import MPI'
    ```

### 2024-05-15

#### `frameworks/2023.12.15.001.lua`

- ✅ works with `ezpz` tests
    - logfile:
    ```bash
    $ aurora_nre_models_frameworks-2024.0 $ realpath . && tail -1 logs/latest
    /lus/gila/projects/Aurora_deployment/foremans/projects/argonne-lcf/Megatron-DeepSpeed
    logs/ws24_ds_stage1_nl10_hs4096_mb2_seq4096_gb48_pp1_tp1_bf16_optadamw_flash/20240515-173423_24_x1921c2s0b0n0/output.log
    ```

> [!note]- Instructions
> ```bash
> module use /soft/modulefiles
> module load frameworks/2023.12.15.001.lua
> mkdir -p venvs/aurora_nre_models_frameworks-2024.0
> python3 -m venv venvs/aurora_nre_models_frameworks-2024.0 --system-site-packages
> source venvs/aurora_nre_models_frameworks-2024.0/bin/activate
> # IDEX
> # ?? cd intel-extension-for-deepspeed
> # ?? python3 -m pip install -r requirements.txt
> pip install intel_extension_for_pytorch_deepspeed\=\=2.1.30 -f https://pytorch-extension.intel.com/release-whl/stable/xpu/us/intel-extension-for-pytorch-deepspeed/
> 
> # ezpz
> git clone https://github.com/saforem2/ezpz ; cd ezpz
> python3 -m pip install -e . --require-virtualenv
> 
> # DeepSpeed
> git clone https://github.com/microsoft/DeepSpeed.git
> cd DeepSpeed
> git remote add yizhou_ds https://github.com/YizhouZ/DeepSpeed.git
> git fetch yizhou_ds
> git checkout yizhou/kernel_path
> pip install -r requirements/requirements.txt
> python setup.py develop |& tee build.log
> 
> # transformers + other deps
> python3 -m pip install intel-extension-for-transformers transformers bitsandbytes sentencepiece neural-speed --upgrade --require-virtualenv
> python3 -m pip install xgboost --force-reinstall --upgrade
> python3 -m pip install einops
> 
> cd /gila/Aurora_deployment/foremans/projects/argonne-lcf/Megatron-DeepSpeed
> ```

####  `frameworks_2024_5_v2`

- ❌ still broken

### 2024-05-14

- ✅`flash-attn` issue on Sunspot **resolved** (??):
    - Using new: `{bash} module use -a /home/jmitche1/anl_release/2024/q2 ; module load frameworks_2024_5_v2`
    - \[No flash\] W&B Run: [earthy-wave-1830](https://wandb.ai/aurora_gpt/AuroraGPT/runs/120ln0b4/overview?nw=nwuserforemans)
    - \[flash\] W&B Run: [youthful-river-1832](https://wandb.ai/aurora_gpt/AuroraGPT/runs/716r5rnq/overview?nw=nwuserforemans)
![#invert](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-fix-sunspot.png)

### 2024-05-08

- New Frameworks Release on Sunspot
	- `{bash} module use -a /home/jmitche1/anl_release/2024/q2`
	- `{bash} module load frameworks_2024_5.lua`
	- Install Instructions:
		- `git clone https://github.com/saforem2/ezpz/ ; python3 -m pip install -e ezpz`
		- Need to `pip install tensorboard, ipython, sentenceipece`
    - Issues:
		-  trying with `NO_FLASH_ATTN` gives:

- Resolved ?? `flash-attn` issue on Sunspot
	![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/ScreenShot-2024-05-07-122338@2x.png)

#### Polaris

- Improved performance with @Huihuo's new NCCL OFI plugin

	```bash
    $ export NCCL_CROSS_NIC=1
    $ export NCCL_COLLNET_ENABLE=1
    $ export NCCL_NET="AWS Libfabric"
    $ export LD_LIBRARY_PATH=/soft/libraries/aws-ofi-nccl/v1.9.1-aws/lib:$LD_LIBRARY_PATH
    $ export LD_LIBRARY_PATH=/soft/libraries/hwloc/lib/:$LD_LIBRARY_PATH
    $ export FI_CXI_DISABLE_HOST_REGISTER=1
    $ export FI_MR_CACHE_MONITOR=userfaultfd
    $ export FI_CXI_DEFAULT_CQ_SIZE=131072
	```

	![#invert](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/ScreenShot-2024-05-08-090847@2x.png)

## 2024-04

### 2024-04-30

#### Sunspot

- & Working @ 16 Nodes with full dolma dataset
    - `pbslogs/8994573.amn-0001-2024-04-30-181250.log`

- 09:11 p.m.:
```bash
    # [09:10:47 PM] [foremans@uan-0001] ~/q/llm.devkit/Megatron-DeepSpeed  polaris-cuda122 !3 ?61 q4-drop
    $ qsme
    
    amn-0001:
                                                                     Req'd  Req'd   Elap
    Job ID               Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
    -------------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
    8994573.amn-0001     foremans diag     train_agp* 168666  16 33*    --  06:00 R 02:57
    8994587.amn-0001     foremans diag     train_agp* 199008  32 66*    --  06:00 R 00:08
    8994603.amn-0001     foremans diag     train_agp* 196397   4 832    --  02:00 R 01:20
    8994609.amn-0001     foremans diag     train_agp*    --   32 66*    --  06:00 Q   --
    ```

- Working @ 4 Nodes with full dolma dataset
    - `pbslogs/8994603.amn-0001-2024-04-30-194957.log`

- Jobs (sometimes?) seem to get stuck @

	```bash
    [2024-04-30 21:03:22,195] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
	```

##### Older
- Run @ 16 Nodes, seems to get hung @ `{bash} > building indices for blendable datasets...`

- Waiting:

```bash
    # [07:23:43 PM] [foremans@uan-0001] ~/q/llm.devkit/Megatron-DeepSpeed  polaris-cuda122 !3 ?57 q4-drop
    $ qsme
    
    amn-0001:
                                                                     Req'd  Req'd   Elap
    Job ID               Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
    -------------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
    8994573.amn-0001     foremans diag     train_agp* 168666  16 33*    --  06:00 R 01:10
    8994587.amn-0001     foremans diag     train_agp*    --   32 66*    --  06:00 Q   --
    ```

#### MBS Tests

- 2 Nodes, 10 Layers

| MBS | GAS | TFLOPs |
| :-: | :-: | :----: |
|  4  |  1  | 64.099 |
|  4  |  8  | 92.122 |
|     |     |        |
|  8  |  1  | 77.115 |
|  8  |  8  | 94.537 |
|     |     |        |
| 16  |  1  | 87.362 |
| 16  |  8  | 97.625 |

#### Polaris

- Waiting...
    - Submitted 48 Node jobs:
        - `1880760` with `{bash} TP=1 MICRO_BATCH=4`
        - `1880794` with `{bash} TP=2 MICRO_BATCH=4`

	```bash
    	$ qsme
        
        polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov:
                                                                         Req'd  Req'd   Elap
        Job ID               Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
        -------------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
        1880760.polaris-pbs* foremans medium   train_agp*    --   48 30*    --  06:00 Q   --
        1880794.polaris-pbs* foremans medium   train_agp*    --   48 30*    --  06:00 Q   --
    	```

> [!info]- NCCL Timeout On Polaris
> - Using:
>
>     ```bash
>     $ export NCCL_NET_GDR_LEVEL=PHB
>     export NCCL_CROSS_NIC=1
>     export NCCL_COLLNET_ENABLE=1
>     export NCCL_NET="AWS Libfabric"
>     export LD_LIBRARY_PATH=/soft/libraries/aws-ofi-nccl/v1.9.1-aws/lib:$LD_LIBRARY_PATH
>     export LD_LIBRARY_PATH=/soft/libraries/hwloc/lib/:$LD_LIBRARY_PATH
>     export FI_CXI_DISABLE_HOST_REGISTER=1
>     export FI_MR_CACHE_MONITOR=userfaultfd
>     export FI_CXI_DEFAULT_CQ_SIZE=131072
>     ```
>
> - Output:
>
>     ```bash
>     
>     x3203c0s25b1n0:322638:323016 [0] NCCL INFO comm 0x55df01b24dd0 rank 24 nranks 32 cudaDev 0 nvmlDev 0 busId 7000 commId 0x2114bc51af4fb978 - Init COMPLETE
>     [2024-04-30 22:06:35][INFO][training:184] - time to initialize megatron (seconds)=12.987
>     [2024-04-30 22:06:35][INFO][training:73] - [after megatron is initialized] datetime=2024-04-30 22:06:35
>     [rank25]:[E ProcessGroupNCCL.cpp:1316] [PG 0 Rank 25] Heartbeat monitor timed out! Process will be terminated after dumping debug info. workMetaList_.size()=2
>     [rank25]:[E ProcessGroupNCCL.cpp:1153] [PG 0 Rank 25] ProcessGroupNCCL preparing to dump debug info.
>     [rank25]:[F ProcessGroupNCCL.cpp:1169] [PG 0 Rank 25] [PG 0 Rank 25] ProcessGroupNCCL's watchdog got stuck for 600 seconds without making progress in monitoring enqueued collectives. This typically indicates a NCCL/CUDA API hang blocking the watchdog, and could be triggered by another thread holding the GIL inside a CUDA api, or other deadlock-prone behaviors.If you suspect the watchdog is not actually stuck and a longer timeout would help, you can either increase the timeout (TORCH_NCCL_HEARTBEAT_TIMEOUT_SEC) to a larger value or disable the heartbeat monitor (TORCH_NCCL_ENABLE_MONITORING=0).If either of aforementioned helps, feel free to file an issue to PyTorch about the short timeout or false positive abort; otherwise, please attempt to debug the hang. workMetaList_.size() = 2
>     x3203c0s25b1n0.hsn.cm.polaris.alcf.anl.gov: rank 25 died from signal 6 and dumped core
>     ```
>
>
- Tested:
    - Testing with 48 Nodes in interactive job w/
        - `{bash} TP=1`, `{bash} ZERO=1`, `{bash} MBS=4`, + full dolma dataset
        - hangs at `{bash} >  building indices for blendable datasets...`
    - Need to test w/ Huihuo's NCCL plugin
        - `{bash} 1881018.polaris-pbs* foremans debug-s* train_agp*    --    8 512    --  01:00 Q   --`
            - logfile @ `{bash} logs/ds_stage1_nl32_hs4096_mb2_seq4096_gb512_pp1_tp1_fp16_optadamwschedulefree/20240430-213501_32_x3203c0s31b0n0/output.log`
    - Tested @ 48 Nodes with `{bash} DATA_FILE_LIST=books.txt`
        - `{bash} TP=1`, `{bash} ZERO_STAGE=1`, `{bash} MICRO_BATCH=4`
        - `{bash} LOGFILE=pbslogs/1880277`
    - Tested @ 16 Nodes with `{bash} books.txt`
        - `{bash} TP=1`,

### 2024-04-25

```bash micromamba-polaris-cu122.sh
$ ssh $(qstat -u $USER -Efan | grep x3 | sed "s/\ \ \ //g" | sed 's/\/0\*64//g' | sed "s/+/\n/g" | tail -1)
$ export MAMBA_ROOT_PREFIX=/eagle/argonne_tpc/micromamba && eval "$("${MAMBA_ROOT_PREFIX}/bin/micromamba" shell hook -s posix)"
$ mm create --name test-2024-04-25 -c pytorch -c nvidia -c conda-forge -c defaults python=3.11 --root-prefix "${MAMBA_ROOT_PREFIX}" # "${MAMBA_ROOT_PREFIX}/.micromambarc" --root-prefix "${MAMBA_ROOT_PREFIX}" --name 2024-04-20 -c pytorch -c nvidia -c conda-forge -c defaults python cmake ninja pytorch torchvision torchaudio "pytorch-cuda==11.8"
$ mm activate test-2024-04-25
$ module load PrgEnv-gnu
$ module list
# Currently Loaded Modules:
#   1) libfabric/1.15.2.0   3) perftools-base/23.12.0   5) gcc-native/12.3   7) cray-dsmml/0.2.2    9) cray-pmi/6.1.13  11) cray-libpals/1.3.4
#   2) craype-network-ofi   4) darshan/3.4.4            6) craype/2.7.30     8) cray-mpich/8.1.28  10) cray-pals/1.3.4  12) PrgEnv-gnu/8.5.0
$ CRAY_CPU_TARGET=x86-64 MPICH_GPU_SUPPORT_ENABLED=1 uv pip install --force-reinstall --no-cache-dir --no-binary=mpi4py deepspeed torch torchvision torchaudio transformers einops appdirs ninja sentencepiece ipython setuptools pybind11 mpi4py toolong schedulefree
```

`{bash}export PBS_NODEFILE=hostfile`

### 2024-04-24

#### \[aGPT\] Co-Leads Sync

- Initial deadline by **end of June**
    - Want to have baseline mode finished + working on training with Science data
    - By end of May:
        - Want `v0` pfinished
    - Polaris under maintenance this week
- Will continue training once Polaris is back online
- Can only train as fast as we get through the queue

### 2024-04-23

> [!tip]- Sirius @ ALCF
>
> ```bash
> # [01:49:21 PM] [foremans@sirius-uan-0002] ~ cu122 1m 8s
> $ ssh $(qstat -x -f $(qstat -u $USER | tail -1 | sed "s/\..*$//g") | grep exec_host | sed "s/exec_host\ =\ //g" | sed "s/\/0\*64.*$//g")
> Last login: Tue Apr 23 18:48:12 2024 from sirius-uan-0002.hsn.cm.sirius.alcf.anl.gov
> ┌──────────────────────────────────────────────────────────────────
> │ [Hosts]:
> │     • [host:0] - x3200c0s13b1n0.hsn.cm.sirius.alcf.anl.gov
> │     • [host:1] - x3200c0s19b0n0.hsn.cm.sirius.alcf.anl.gov
> └──────────────────────────────────────────────────────────────────
> ┌──────────────────────────────────────────────────────────────────
> │ [DIST INFO]:
> │     • Loading job env from: /home/foremans/.pbsenv
> │     • HOSTFILE: /var/spool/pbs/aux/8224.sirius-pbs-0001.hsn.cm.sirius.alcf.anl.gov
> │     • NHOSTS: 2
> │     • NGPU_PER_HOST: 4
> │     • NGPUS (NHOSTS x NGPU_PER_HOST): 8
> │     • WORLD_SIZE: 8
> │     • DIST_LAUNCH: mpiexec --verbose --envall -n 8 -ppn 4 --hostfile /var/spool/pbs/aux/8224.sirius-pbs-0001.hsn.cm.sirius.alcf.anl.gov
> └──────────────────────────────────────────────────────────────────
> ┌──────────────────────────────────────────────────────────────────
> │ [Launch]:
> │     • Use: 'launch' (=mpiexec --verbose --envall -n 8 -ppn 4 --hostfile /var/spool/pbs/aux/8224.sirius-pbs-0001.hsn.cm.sirius.alcf.anl.gov)
> │       to launch job
> └──────────────────────────────────────────────────────────────────
> # [01:49:26 PM] [foremans@x3200c0s13b1n0] ~
> $ export MAMBA_ROOT_PREFIX=/lus/tegu/projects/PolarisAT/foremans/micromamba && eval "$("${MAMBA_ROOT_PREFIX}/bin/micromamba" shell hook --shell zsh)"
> zsh: exit 1
> zsh: exit 1
> zsh: exit 1
> 
> # [01:49:31 PM] [foremans@x3200c0s13b1n0] ~
> $ mm activate 2024-04-23
> 
> # [01:49:36 PM] [foremans@x3200c0s13b1n0] ~ 2024-04-23
> $ launch python3 -m ezpz.test_dist
> Read only 28 bytes from /etc/pals/server_key.pub, expected 40
> Couldnt read server key, disabling ZeroMQ CURVE security
> Connected to tcp://x3200c0s13b1n0.hsn.cm.sirius.alcf.anl.gov:7919
> Found executable /lus/tegu/projects/PolarisAT/foremans/micromamba/envs/2024-04-23/bin/python3
> Launching application be844a13-05ff-478d-b059-74e1776d79b4
> Using PMI port 55041,55042
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=3/7][local_rank=3/3][node=1/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=2/7][local_rank=2/3][node=0/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=1/7][local_rank=1/3][node=1/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=5/7][local_rank=1/3][node=1/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=4/7][local_rank=0/3][node=0/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=6/7][local_rank=2/3][node=0/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=7/7][local_rank=3/3][node=1/1]
> [2024-04-23 13:49:40][INFO][dist:290] - [device='cuda'][rank=0/7][local_rank=0/3][node=0/1]
> [2024-04-23 13:49:40][WARNING][dist:296] - Using [8 / 8] available "cuda" devices !!
> [2024-04-23 13:49:40][INFO][test_dist:46] - DIST_INIT={'world_size': 8, 'rank': 0, 'local_rank': 0}
> [2024-04-23 13:49:41][INFO][test_dist:84] - model=Network(
>   (layers): Sequential(
>     (0): Linear(in_features=128, out_features=1024, bias=True)
>     (1): Linear(in_features=1024, out_features=512, bias=True)
>     (2): Linear(in_features=512, out_features=256, bias=True)
>     (3): Linear(in_features=256, out_features=128, bias=True)
>     (4): Linear(in_features=128, out_features=128, bias=True)
>   )
> )
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=0, loss=2757.20654, dt=0.176, dtf=0.081, dtb=0.094
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=1, loss=2086.92871, dt=0.002, dtf=0.001, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=2, loss=1586.07324, dt=0.002, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=3, loss=1239.61047, dt=0.002, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=4, loss=1050.91357, dt=0.001, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=5, loss=891.80029, dt=0.001, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=6, loss=786.97595, dt=0.001, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=7, loss=746.01270, dt=0.001, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=8, loss=753.29138, dt=0.001, dtf=0.000, dtb=0.001
> [2024-04-23 13:49:43][INFO][test_dist:126] - iter=9, loss=737.17511, dt=0.001, dtf=0.000, dtb=0.001
> ```

### 2024-04-22

#### `ipex.Lamb` on Sunspot

- Seems to crash with `NaN` after first training iteration ??

### 2024-04-21

> [!note]- 1B Model: 160 TFLOPs !!
>
> ```bash
> [02:43:36 AM] [foremans@x3014c0s1b0n0] /eagle/a/f/p/ar/Megatron-DeepSpeed  main !12 ?7 cu118-pt221 4m 20s ✘ INT
> cu118-pt221   PBS_O_WORKDIR=$(pwd) DATA_FILE_LIST=./ALCF/data-lists/polaris/data_file_list_wiki.txt TRAIN_ITERS=320000 ZERO_STAGE=1 GRAD_ACC_STEPS=8 MICRO_BATCH=8 NLAYERS=10 LR=0.0008 OPT=adamwschedulefree bash train_llama_alcf.sh --lr-warmup-fraction 0.050
> source-ing /lus/eagle/projects/argonne_tpc/foremans/projects/argonne-lcf/Megatron-DeepSpeed/ALCF/helpers.sh
> Using: /eagle/datascience/foremans/miniconda3/envs/cu118-pt221/bin/deepspeed[python] Using: /lus/eagle/projects/argonne_tpc/foremans/projects/argonne-lcf/Megatron-DeepSpeed/venvs/polaris/cu118-pt221/bin/python3
> Saving {PATH, LD_LIBRARY_PATH, htt{p,ps}_proxy, CFLAGS, PYTHONUSERBASE} to .deepspeed_env
> Found ezpz!
> /lus/eagle/projects/argonne_tpc/foremans/projects/argonne-lcf/Megatron-DeepSpeed/deps/ezpz/src/ezpz/__init__.py
> Has ezpz installed. Nothing to do.
> Done with ezpz.
> ┌───────────────────────────────────────────────────────────────────
> │ Writing PBS vars to /home/foremans/.pbsenv
> │ HOSTFILE: /var/spool/pbs/aux/1874210.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov
> │ NHOSTS: 2
> │ NGPU_PER_HOST: 4 GPUs per host
> │ NGPUS: 8 GPUs total
> └───────────────────────────────────────────────────────────────────
> ┌───────────────────────────────────────────────────────────────────
> │ [DIST INFO]:
> │   • Writing Job info to /home/foremans/.pbsenv
> │     • HOSTFILE: /var/spool/pbs/aux/1874210.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov
> │     • NHOSTS: 2
> │     • NGPU_PER_HOST: 4
> │     • NGPUS = (NHOSTS * NGPU_PER_HOST) = 8
> └──────────────────────────────────────────────────────────────────
> ┌──────────────────────────────────────────────────────────────────
> │ [Hosts]:
> │       • x3014c0s19b1n0.hsn.cm.polaris.alcf.anl.gov, x3014c0s1b0n0.hsn.cm.polaris.alcf.anl.gov
> │     • [host:0] - x3014c0s19b1n0.hsn.cm.polaris.alcf.anl.gov
> │     • [host:1] - x3014c0s1b0n0.hsn.cm.polaris.alcf.anl.gov
> └──────────────────────────────────────────────────────────────────
> 
> # ... clipped ...
> 
> [2024-04-21 02:44:01,174] [INFO] [comm.py:637:init_distributed] cdb=None
> [2024-04-21 02:44:01,174] [INFO] [comm.py:637:init_distributed] cdb=None
> wandb: Currently logged in as: foremans (aurora_gpt). Use `wandb login --relogin` to force relogin
> wandb: wandb version 0.16.6 is available!  To upgrade, please run:
> wandb:  $ pip install wandb --upgrade
> wandb: Tracking run with wandb version 0.16.5
> wandb: Run data is saved locally in /lus/eagle/projects/argonne_tpc/foremans/projects/argonne-lcf/Megatron-DeepSpeed/wandb/run-20240421_024402-4z5ap32w
> wandb: Run `wandb offline` to turn off syncing.
> wandb: Syncing run swift-morning-1398
> wandb: ⭐️ View project at https://wandb.ai/aurora_gpt/AuroraGPT
> wandb: 🚀 View run at https://wandb.ai/aurora_gpt/AuroraGPT/runs/4z5ap32w/workspace
> [2024-04-21 02:44:06][INFO][dist:782] - W&B RUN: [swift-morning-1398](https://wandb.ai/aurora_gpt/AuroraGPT/runs/4z5ap32w)
> [2024-04-21 02:44:06][INFO][dist:810] - Running on machine='Polaris'
> using world size: 8, data-parallel-size: 4, sequence-parallel size: 1, tensor-model-parallel size: 2, pipeline-model-parallel size: 1
> using torch.float16 for parameters ...
> 
> # ... clipped ...
> 
> [Rank 1] (after 1 iterations) memory (MB) | allocated: 4866.666015625 | max allocated: 14024.81396484375 | reserved: 17240.0 | max reserved: 17240.0
> [2024-04-21 02:45:08][INFO][training:1251] -  iteration=       1/  317892 | consumed_samples=         256 | consumed_tokens=     1048576 | elapsed_time_per_iteration_ms=17711.7 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.208768 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=14.454 | tokens_per_gpu_per_second_tgs=7400.298 | TFLOPs=144.87 |
> [Rank 0] (after 1 iterations) memory (MB) | allocated: 4866.666015625 | max allocated: 14024.81396484375 | reserved: 17240.0 | max reserved: 17240.0
> [2024-04-21 02:45:24,650] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 536.33 | optimizer_gradients: 4.05 | optimizer_step: 19.34
> [2024-04-21 02:45:24,651] [INFO] [logging.py:96:log_dist] [Rank 0] step=2, skipped=0, lr=[1.0066311829174689e-07, 1.0066311829174689e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:45:24,651] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3859.38 | bwd_microstep: 11267.96 | bwd_inner_microstep: 10508.40 | bwd_allreduce_microstep: 759.39 | step_microstep: 829.18
> [2024-04-21 02:45:24,652] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3859.30 | bwd: 11267.97 | bwd_inner: 10508.40 | bwd_allreduce: 759.40 | step: 829.19
> [2024-04-21 02:45:24][INFO][training:1251] -  iteration=       2/  317892 | consumed_samples=         512 | consumed_tokens=     2097152 | elapsed_time_per_iteration_ms=16030.6 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.208171 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.969 | tokens_per_gpu_per_second_tgs=8176.383 | TFLOPs=160.07 |
> [2024-04-21 02:45:40,722] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 559.27 | optimizer_gradients: 4.05 | optimizer_step: 19.35
> [2024-04-21 02:45:40,722] [INFO] [logging.py:96:log_dist] [Rank 0] step=3, skipped=0, lr=[1.5099467743762034e-07, 1.5099467743762034e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:45:40,722] [INFO] [timer.py:260:stop] epoch=0/micro_step=3/global_step=3, RunningAvgSamplesPerSec=74.68528989415996, CurrSamplesPerSec=74.68528989415996, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:45:40,723] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3865.99 | bwd_microstep: 11249.42 | bwd_inner_microstep: 10520.18 | bwd_allreduce_microstep: 729.08 | step_microstep: 888.44
> [2024-04-21 02:45:40,723] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3865.91 | bwd: 11249.43 | bwd_inner: 10520.18 | bwd_allreduce: 729.09 | step: 888.45
> [2024-04-21 02:45:40][INFO][training:1251] -  iteration=       3/  317892 | consumed_samples=         768 | consumed_tokens=     3145728 | elapsed_time_per_iteration_ms=16071.8 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.205435 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.929 | tokens_per_gpu_per_second_tgs=8155.393 | TFLOPs=159.66 |
> [2024-04-21 02:45:56,791] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 560.12 | optimizer_gradients: 4.05 | optimizer_step: 19.35
> [2024-04-21 02:45:56,791] [INFO] [logging.py:96:log_dist] [Rank 0] step=4, skipped=0, lr=[2.0132623658349378e-07, 2.0132623658349378e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:45:56,792] [INFO] [timer.py:260:stop] epoch=0/micro_step=4/global_step=4, RunningAvgSamplesPerSec=74.7483926623704, CurrSamplesPerSec=74.81160215378233, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:45:56,792] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3871.07 | bwd_microstep: 11294.43 | bwd_inner_microstep: 10544.17 | bwd_allreduce_microstep: 750.09 | step_microstep: 865.13
> [2024-04-21 02:45:56,793] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3870.98 | bwd: 11294.43 | bwd_inner: 10544.17 | bwd_allreduce: 750.10 | step: 865.13
> [2024-04-21 02:45:56][INFO][training:1251] -  iteration=       4/  317892 | consumed_samples=        1024 | consumed_tokens=     4194304 | elapsed_time_per_iteration_ms=16069.2 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.205074 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.931 | tokens_per_gpu_per_second_tgs=8156.733 | TFLOPs=159.68 |
> [2024-04-21 02:46:12,844] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 539.06 | optimizer_gradients: 4.06 | optimizer_step: 19.35
> [2024-04-21 02:46:12,844] [INFO] [logging.py:96:log_dist] [Rank 0] step=5, skipped=0, lr=[2.516577957293672e-07, 2.516577957293672e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:46:12,845] [INFO] [timer.py:260:stop] epoch=0/micro_step=5/global_step=5, RunningAvgSamplesPerSec=75.00453690967313, CurrSamplesPerSec=75.522128204809, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:46:12,845] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3868.22 | bwd_microstep: 11270.09 | bwd_inner_microstep: 10529.72 | bwd_allreduce_microstep: 740.20 | step_microstep: 839.35
> [2024-04-21 02:46:12,846] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3868.14 | bwd: 11270.09 | bwd_inner: 10529.72 | bwd_allreduce: 740.21 | step: 839.36
> [2024-04-21 02:46:12][INFO][training:1251] -  iteration=       5/  317892 | consumed_samples=        1280 | consumed_tokens=     5242880 | elapsed_time_per_iteration_ms=16053.0 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.203266 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.947 | tokens_per_gpu_per_second_tgs=8164.952 | TFLOPs=159.84 |
> [2024-04-21 02:46:28,937] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 565.20 | optimizer_gradients: 4.05 | optimizer_step: 19.34
> [2024-04-21 02:46:28,937] [INFO] [logging.py:96:log_dist] [Rank 0] step=6, skipped=0, lr=[3.019893548752407e-07, 3.019893548752407e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:46:28,937] [INFO] [timer.py:260:stop] epoch=0/micro_step=6/global_step=6, RunningAvgSamplesPerSec=74.99879723364612, CurrSamplesPerSec=74.98158347505746, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:46:28,938] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3869.84 | bwd_microstep: 11244.59 | bwd_inner_microstep: 10526.45 | bwd_allreduce_microstep: 717.97 | step_microstep: 892.29
> [2024-04-21 02:46:28,938] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3869.76 | bwd: 11244.59 | bwd_inner: 10526.45 | bwd_allreduce: 717.98 | step: 892.30
> [2024-04-21 02:46:28][INFO][training:1251] -  iteration=       6/  317892 | consumed_samples=        1536 | consumed_tokens=     6291456 | elapsed_time_per_iteration_ms=16092.2 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.201191 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.908 | tokens_per_gpu_per_second_tgs=8145.085 | TFLOPs=159.46 |
> [2024-04-21 02:46:45,043] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 554.27 | optimizer_gradients: 4.05 | optimizer_step: 19.35
> [2024-04-21 02:46:45,044] [INFO] [logging.py:96:log_dist] [Rank 0] step=7, skipped=0, lr=[3.523209140211141e-07, 3.523209140211141e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:46:45,044] [INFO] [timer.py:260:stop] epoch=0/micro_step=7/global_step=7, RunningAvgSamplesPerSec=74.95169716365959, CurrSamplesPerSec=74.76388698858936, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:46:45,045] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3872.93 | bwd_microstep: 11264.22 | bwd_inner_microstep: 10532.44 | bwd_allreduce_microstep: 731.61 | step_microstep: 885.62
> [2024-04-21 02:46:45,045] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3872.85 | bwd: 11264.23 | bwd_inner: 10532.44 | bwd_allreduce: 731.62 | step: 885.62
> [2024-04-21 02:46:45][INFO][training:1251] -  iteration=       7/  317892 | consumed_samples=        1792 | consumed_tokens=     7340032 | elapsed_time_per_iteration_ms=16106.8 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.188668 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.894 | tokens_per_gpu_per_second_tgs=8137.692 | TFLOPs=159.31 |
> [2024-04-21 02:47:01,222] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 568.50 | optimizer_gradients: 4.05 | optimizer_step: 19.34
> [2024-04-21 02:47:01,222] [INFO] [logging.py:96:log_dist] [Rank 0] step=8, skipped=0, lr=[4.0265247316698756e-07, 4.0265247316698756e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:47:01,222] [INFO] [timer.py:260:stop] epoch=0/micro_step=8/global_step=8, RunningAvgSamplesPerSec=74.82504909687192, CurrSamplesPerSec=74.19817500468169, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:47:01,223] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3879.97 | bwd_microstep: 11310.90 | bwd_inner_microstep: 10561.56 | bwd_allreduce_microstep: 749.17 | step_microstep: 880.73
> [2024-04-21 02:47:01,223] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3879.89 | bwd: 11310.91 | bwd_inner: 10561.56 | bwd_allreduce: 749.18 | step: 880.74
> [2024-04-21 02:47:01][INFO][training:1251] -  iteration=       8/  317892 | consumed_samples=        2048 | consumed_tokens=     8388608 | elapsed_time_per_iteration_ms=16178.1 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.181074 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.824 | tokens_per_gpu_per_second_tgs=8101.811 | TFLOPs=158.61 |
> [2024-04-21 02:47:17,401] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 552.69 | optimizer_gradients: 4.06 | optimizer_step: 19.36
> [2024-04-21 02:47:17,401] [INFO] [logging.py:96:log_dist] [Rank 0] step=9, skipped=0, lr=[4.5298403231286103e-07, 4.5298403231286103e-07], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-21 02:47:17,402] [INFO] [timer.py:260:stop] epoch=0/micro_step=9/global_step=9, RunningAvgSamplesPerSec=74.84645585628223, CurrSamplesPerSec=74.9751540746784, MemAllocated=4.75GB, MaxMemAllocated=15.59GB
> [2024-04-21 02:47:17,402] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 3880.08 | bwd_microstep: 11312.61 | bwd_inner_microstep: 10561.38 | bwd_allreduce_microstep: 751.06 | step_microstep: 836.26
> [2024-04-21 02:47:17,403] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 3880.01 | bwd: 11312.61 | bwd_inner: 10561.38 | bwd_allreduce: 751.07 | step: 836.26
> [2024-04-21 02:47:17][INFO][training:1251] -  iteration=       9/  317892 | consumed_samples=        2304 | consumed_tokens=     9437184 | elapsed_time_per_iteration_ms=16179.4 | learning_rate=0.000000 | global_batch_size=  256 | lm loss=11.146455 | loss_scale=65536.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=15.823 | tokens_per_gpu_per_second_tgs=8101.150 | TFLOPs=158.60 |
> 
> ```

### 2024-04-20

- ~ 145 TFLOPS for 1.2B Model [autumn-plant-1373](https://wandb.ai/aurora_gpt/AuroraGPT/runs/t7uh66g4/workspace?nw=nwuserforemans)

#### MicroMamba on Polaris

> [!highlight]- \[🦠 + 🐍\]
> ## Instructions
>
> - `mm activate 2024-04-20`
>
> - to Activate:
>
> ```bash
>   $ export MAMBA_ROOT_PREFIX=/eagle/argonne_tpc/foremans/micromamba
>   $ eval "$(${MAMBA_ROOT_PREFIX}/bin/micromamba shell hook -s posix)"
>   $ alias mm="micromamba"
>   ```
>
> - Running on Polaris:
>
> ```bash
>     [07:25:47 PM] [foremans@polaris-login-02] /eagle/a/f/micromamba 25m 31s
>     $ ssh $(qstat -u $USER -Efan | grep x3 | sed "s/\ \ \ //g" | sed 's/\/0\*64//g' | sed "s/+/\n/g" | tail -1)
>     Last login: Sun Apr 21 00:00:16 2024 from polaris-login-02.hsn.cm.polaris.alcf.anl.gov
>     Compute node detected !!
>     No PBS_NODEFILE detected in environment...
>     Trying: `source getjobenv`
>     ┌──────────────────────────────────────────────────────────────────
>     │ [Hosts]:
>     │     • [host:0] - x3005c0s13b0n0.hsn.cm.polaris.alcf.anl.gov
>     │     • [host:1] - x3005c0s25b1n0.hsn.cm.polaris.alcf.anl.gov
>     └──────────────────────────────────────────────────────────────────
>     ┌──────────────────────────────────────────────────────────────────
>     │ [DIST INFO]:
>     │     • Loading job env from: /home/foremans/.pbsenv
>     │     • HOSTFILE: /var/spool/pbs/aux/1873952.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov
>     │     • NHOSTS: 2
>     │     • NGPU_PER_HOST: 4
>     │     • NGPUS (NHOSTS x NGPU_PER_HOST): 8
>     │     • WORLD_SIZE: 8
>     │     • DIST_LAUNCH: mpiexec --verbose --envall -n 8 -ppn 4 --hostfile /var/spool/pbs/aux/1873952.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov
>     └──────────────────────────────────────────────────────────────────
>     ┌──────────────────────────────────────────────────────────────────
>     │ [Launch]:
>     │     • Use: 'launch' (=mpiexec --verbose --envall -n 8 -ppn 4 --hostfile /var/spool/pbs/aux/1873952.polaris-pbs-01.hsn.cm.polaris.alcf.anl.gov)
>     │       to launch job
>     └──────────────────────────────────────────────────────────────────
>     [07:25:57 PM] [foremans@x3005c0s25b1n0] ~
>     $ export MAMBA_ROOT_PREFIX=/eagle/argonne_tpc/foremans/micromamba ; eval "$(${MAMBA_ROOT_PREFIX}/bin/micromamba shell hook -s posix)" ; alias mm="micromamba"
>     zsh: exit 1
>     zsh: exit 1
>     
>     [07:26:00 PM] [foremans@x3005c0s25b1n0] ~
>     $ mm activate 2024-04-20
>     ```

> [!success]- Working `conda` on Polaris !!
> - Run Log:
> ```bash
> [07:21:51 PM] [foremans@x3005c0s25b1n0] /eagle/a/f/p/ar/Megatron-DeepSpeed  main !5 ?7 2024-04-20 8s
> $ mm install libssh
> conda-forge/linux-64                                        Using cache
> conda-forge/noarch                                          Using cache
> nodefaults/linux-64                                           No change
> nodefaults/noarch                                             No change
> 
> Pinned packages:
>   - python 3.11.*
> 
> 
> Transaction
> 
>   Prefix: /lus/eagle/projects/datascience/foremans/miniconda3/envs/2024-04-20
> 
>   All requested packages already installed
> 
> 
> Transaction starting
> 
> Transaction finished
> 
> To activate this environment, use:
> 
>     micromamba activate 2024-04-20
> 
> Or to execute a single command in this environment, use:
> 
>     micromamba run -n 2024-04-20 mycommand
> [07:21:59 PM] [foremans@x3005c0s25b1n0] /eagle/a/f/p/ar/Megatron-DeepSpeed  main !5 ?7 2024-04-20
> $ mm remove mpi
> Transaction
> 
>   Prefix: /lus/eagle/projects/datascience/foremans/miniconda3/envs/2024-04-20
> 
>   Removing specs:
> 
>    - mpi
> 
> 
>   Package      Version  Build            Channel          Size
> ────────────────────────────────────────────────────────────────
>   Remove:
> ────────────────────────────────────────────────────────────────
> 
>   - mpi4py       3.1.6  py311he9ffdee_0  conda-forge     567kB
>   - impi_rt  2021.12.0  ha770c72_535     conda-forge      37MB
>   - mpi            1.0  impi             conda-forge       7kB
> 
>   Summary:
> 
>   Remove: 3 packages
> 
>   Total download: 0 B
> 
> ────────────────────────────────────────────────────────────────
> 
> 
> Confirm changes: [Y/n] y
> 
> Transaction starting
> Unlinking mpi4py-3.1.6-py311he9ffdee_0
> Unlinking impi_rt-2021.12.0-ha770c72_535
> Unlinking mpi-1.0-impi
> 
> Transaction finished
> 
> To activate this environment, use:
> 
>     micromamba activate 2024-04-20
> 
> Or to execute a single command in this environment, use:
> 
>     micromamba run -n 2024-04-20 mycommand
> 
> $ module load gcc ; MPICC="cc -target-accel=nvidia80" CC=cc uv pip install --force-reinstall --no-cache-dir --no-binary=mpi4py mpi4py
> Resolved 1 package in 131ms
> Building mpi4py==3.1.6
>    Built mpi4py==3.1.6
> Downloaded 1 package in 25.97s
> ```
>

### 2024-04-19

- Is the DeepSpeed profiler broken ??
    - Weird Numbers on Sunspot???

> [!bug]- DeepSpeed Profiler
>
> ```bash
> loading blendable dataset index: /lus/gila/projects/Aurora_deployment/foremans/q4-drop_sunspot/llm.devkit/Megatron-DeepSpeed/.cache/data_file_list_pes2o/index-cache/8403e041ceb201c11a42bd6cb57b073c_index.npy
> loading blendable dataset sample index: /lus/gila/projects/Aurora_deployment/foremans/q4-drop_sunspot/llm.devkit/Megatron-DeepSpeed/.cache/data_file_list_pes2o/index-cache/8403e041ceb201c11a42bd6cb57b073c_sample_index.npy
> size of blendable dataset: 11577613 samples
> finished creating GPT datasets ...
> [2024-04-19 13:24:57][INFO][training:73] - [after dataloaders are built] datetime=2024-04-19 13:24:57
> [2024-04-19 13:24:57][INFO][training:259] - done with setup ...
> (min, max) time across ranks (ms):
>     model-and-optimizer-setup ......................: (39957.93, 39960.27)
>     train/valid/test-data-iterators-setup ..........: (7116.11, 7228.99)
> [2024-04-19 13:24:57][INFO][training:264] - training ...
> [2024-04-19 13:24:57][INFO][training:73] - [before the start of training step] datetime=2024-04-19 13:24:57
> [2024-04-19 13:24:58,072] [INFO] [checkpointing.py:540:forward] Activation Checkpointing Information
> [2024-04-19 13:24:58,072] [INFO] [checkpointing.py:541:forward] ----Partition Activations False, CPU CHECKPOINTING False
> [2024-04-19 13:24:58,073] [INFO] [checkpointing.py:542:forward] ----contiguous Memory Checkpointing False with 12 total layers
> [2024-04-19 13:24:58,073] [INFO] [checkpointing.py:544:forward] ----Synchronization False
> [2024-04-19 13:24:58,073] [INFO] [checkpointing.py:545:forward] ----Profiling time in checkpointing False
> [2024-04-19 13:25:17][INFO][utils:145] - Note: detected 208 virtual cores but NumExpr set to maximum of 64, check "NUMEXPR_MAX_THREADS" environment variable.
> [2024-04-19 13:25:17][INFO][utils:148] - Note: NumExpr detected 208 cores but "NUMEXPR_MAX_THREADS" not set, so enforcing safe limit of 8.
> [2024-04-19 13:25:17][INFO][utils:160] - NumExpr defaulting to 8 threads.
> [2024-04-19 13:26:38,107] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 495.69 | optimizer_gradients: 1.73 | optimizer_step: 14.20
> [2024-04-19 13:26:38,108] [INFO] [logging.py:96:log_dist] [Rank 0] step=1, skipped=0, lr=[2.0000000000000003e-06, 2.0000000000000003e-06], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:26:38,109] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 32390.78 | bwd_microstep: 56173.28 | bwd_inner_microstep: 53330.36 | bwd_allreduce_microstep: 2842.47 | step_microstep: 1169.58
> [2024-04-19 13:26:38,109] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 32390.69 | bwd: 56173.16 | bwd_inner: 53330.31 | bwd_allreduce: 2842.52 | step: 1169.60
> [2024-04-19 13:26:38][INFO][training:1251] -  iteration=       1/   10000 | consumed_samples=        1152 | consumed_tokens=     4718592 | elapsed_time_per_iteration_ms=101182.7 | learning_rate=0.000002 | global_batch_size= 1152 | lm loss=11.198063 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=11.385 | tokens_per_gpu_per_second_tgs=1943.099 | TFLOPs=45.34 |
> [Rank 0] (after 1 iterations) memory (MB) | allocated: 5696.2509765625 | max allocated: 17001.390625 | reserved: 19908.0 | max reserved: 19908.0
> [2024-04-19 13:27:45,502] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 126.72 | optimizer_gradients: 1.71 | optimizer_step: 14.14
> [2024-04-19 13:27:45,503] [INFO] [logging.py:96:log_dist] [Rank 0] step=2, skipped=0, lr=[4.000000000000001e-06, 4.000000000000001e-06], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:27:45,504] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9695.97 | bwd_microstep: 48449.79 | bwd_inner_microstep: 45767.68 | bwd_allreduce_microstep: 2681.72 | step_microstep: 150.43
> [2024-04-19 13:27:45,504] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9695.89 | bwd: 48449.69 | bwd_inner: 45767.63 | bwd_allreduce: 2681.72 | step: 150.45
> [2024-04-19 13:27:45][INFO][training:1251] -  iteration=       2/   10000 | consumed_samples=        2304 | consumed_tokens=     9437184 | elapsed_time_per_iteration_ms=67212.1 | learning_rate=0.000004 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=17.140 | tokens_per_gpu_per_second_tgs=2925.188 | TFLOPs=68.26 |
> [2024-04-19 13:28:48,886] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 131.61 | optimizer_gradients: 1.73 | optimizer_step: 14.29
> [2024-04-19 13:28:48,887] [INFO] [logging.py:96:log_dist] [Rank 0] step=3, skipped=0, lr=[6e-06, 6e-06], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:28:48,887] [INFO] [timer.py:260:stop] epoch=0/micro_step=3/global_step=3, RunningAvgSamplesPerSec=151.50460549287803, CurrSamplesPerSec=151.50460549287803, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> [2024-04-19 13:28:48,888] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9288.12 | bwd_microstep: 47613.86 | bwd_inner_microstep: 44920.58 | bwd_allreduce_microstep: 2692.86 | step_microstep: 155.69
> [2024-04-19 13:28:48,888] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9288.04 | bwd: 47613.76 | bwd_inner: 44920.55 | bwd_allreduce: 2692.85 | step: 155.70
> [2024-04-19 13:28:48][INFO][training:1251] -  iteration=       3/   10000 | consumed_samples=        3456 | consumed_tokens=    14155776 | elapsed_time_per_iteration_ms=63383.5 | learning_rate=0.000006 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.175 | tokens_per_gpu_per_second_tgs=3101.882 | TFLOPs=72.38 |
> [2024-04-19 13:29:51,358] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 127.93 | optimizer_gradients: 1.75 | optimizer_step: 14.37
> [2024-04-19 13:29:51,359] [INFO] [logging.py:96:log_dist] [Rank 0] step=4, skipped=0, lr=[8.000000000000001e-06, 8.000000000000001e-06], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:29:51,360] [INFO] [timer.py:260:stop] epoch=0/micro_step=4/global_step=4, RunningAvgSamplesPerSec=151.18121342818228, CurrSamplesPerSec=150.85919900699352, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> [2024-04-19 13:29:51,361] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9294.96 | bwd_microstep: 47634.93 | bwd_inner_microstep: 44940.23 | bwd_allreduce_microstep: 2694.31 | step_microstep: 152.89
> [2024-04-19 13:29:51,361] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9294.88 | bwd: 47634.83 | bwd_inner: 44940.20 | bwd_allreduce: 2694.31 | step: 152.91
> [2024-04-19 13:29:51][INFO][training:1251] -  iteration=       4/   10000 | consumed_samples=        4608 | consumed_tokens=    18874368 | elapsed_time_per_iteration_ms=62472.7 | learning_rate=0.000008 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.440 | tokens_per_gpu_per_second_tgs=3147.104 | TFLOPs=73.44 |
> [2024-04-19 13:29:51,872] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:29:59,257] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:07,079] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:15,150] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:23,204] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:31,219] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:39,285] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:46,642] [INFO] [profiler.py:80:start_profile] Flops profiler started
> [2024-04-19 13:30:54,277] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 134.52 | optimizer_gradients: 1.72 | optimizer_step: 14.45
> [2024-04-19 13:30:54,278] [INFO] [logging.py:96:log_dist] [Rank 0] step=5, skipped=0, lr=[9.999999999999999e-06, 9.999999999999999e-06], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:30:54,278] [INFO] [timer.py:260:stop] epoch=0/micro_step=5/global_step=5, RunningAvgSamplesPerSec=151.12940036412186, CurrSamplesPerSec=151.02588070775124, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> 
> -------------------------- DeepSpeed Flops Profiler --------------------------
> Profile Summary at step 5:
> Notations:
> data parallel size (dp_size), model parallel size(mp_size),
> number of parameters (params), number of multiply-accumulate operations(MACs),
> number of floating-point operations (flops), floating-point operations per second (FLOPS),
> fwd latency (forward propagation latency), bwd latency (backward propagation latency),
> step (weights update latency), iter latency (sum of fwd, bwd and step latency)
> 
> world size:                                                             24
> data parallel size:                                                     24
> model parallel size:                                                    1
> batch size per GPU:                                                     6
> params per GPU:                                                         2.39 B
> params of model = params per GPU * mp_size:                             2.39 B
> fwd MACs per GPU:                                                       55.48 TMACs
> fwd flops per GPU:                                                      110.97 T
> fwd flops of model = fwd flops per GPU * mp_size:                       110.97 T
> fwd latency:                                                            9.34 s
> fwd FLOPS per GPU = fwd flops per GPU / fwd latency:                    11.88 TFLOPS
> bwd latency:                                                            -2.9601e+08 us
> bwd FLOPS per GPU = 2 * fwd flops per GPU / bwd latency:                -7.49758e+17 uFLOPS
> fwd+bwd FLOPS per GPU = 3 * fwd flops per GPU / (fwd+bwd latency):      -1.16128e+18 uFLOPS
> step latency:                                                           158.64 ms
> iter latency:                                                           -2.86511e+08 us
> FLOPS per GPU = 3 * fwd flops per GPU / iter latency:                   -1.16192e+18 uFLOPS
> samples/second:                                                         -0.5
> 
> ----------------------------- Aggregated Profile per GPU -----------------------------
> Top 1 modules in terms of params, MACs or fwd latency at different model depths:
> depth 0:
>     params      - {'GPTModel': '2.39 B'}
>     MACs        - {'GPTModel': '55.48 TMACs'}
>     fwd latency - {'GPTModel': '1.17 s'}
> depth 1:
>     params      - {'TransformerLanguageModel': '2.39 B'}
>     MACs        - {'TransformerLanguageModel': '52.26 TMACs'}
>     fwd latency - {'TransformerLanguageModel': '1.09 s'}
> depth 2:
>     params      - {'ParallelTransformer': '2.13 B'}
>     MACs        - {'ParallelTransformer': '52.26 TMACs'}
>     fwd latency - {'ParallelTransformer': '1.09 s'}
> depth 3:
>     params      - {'ModuleList': '2.13 B'}
>     MACs        - {'ModuleList': '52.26 TMACs'}
>     fwd latency - {'ModuleList': '1.08 s'}
> depth 4:
>     params      - {'ParallelTransformerLayer': '2.13 B'}
>     MACs        - {'ParallelTransformerLayer': '52.26 TMACs'}
>     fwd latency - {'ParallelTransformerLayer': '1.08 s'}
> depth 5:
>     params      - {'ParallelMLP': '1.62 B'}
>     MACs        - {'ParallelMLP': '39.89 TMACs'}
>     fwd latency - {'ParallelAttention': '524.73 ms'}
> 
> ------------------------------ Detailed Profile per GPU ------------------------------
> Each module profile is listed after its name in the following order:
> params, percentage of total params, MACs, percentage of total MACs, fwd latency, percentage of total fwd latency, fwd FLOPS
> 
> Note: 1. A module can have torch.nn.module or torch.nn.functional to compute logits (e.g. CrossEntropyLoss). They are not counted as submodules, thus not to be printed out. However they make up the difference between a parent's MACs (or latency) and the sum of its submodules'.
> 2. Number of floating-point operations is a theoretical estimation, thus FLOPS computed using that could be larger than the maximum system throughput.
> 3. The fwd latency listed in the top module's profile is directly captured at the module forward function in PyTorch, thus it's less than the fwd latency shown above which is captured in DeepSpeed.
> 
> GPTModel(
>   2.39 B = 100% Params, 55.48 TMACs = 100% MACs, 1.17 s = 100% latency, 95.06 TFLOPS
>   (language_model): TransformerLanguageModel(
>     2.39 B = 100% Params, 52.26 TMACs = 94.19% MACs, 1.09 s = 93.7% latency, 95.56 TFLOPS
>     (embedding): Embedding(
>       131.07 M = 5.49% Params, 0 MACs = 0% MACs, 3.26 ms = 0.28% latency, 0 FLOPS
>       (word_embeddings): VocabParallelEmbedding(131.07 M = 5.49% Params, 0 MACs = 0% MACs, 2.11 ms = 0.18% latency, 0 FLOPS)
>       (embedding_dropout): Dropout(0 = 0% Params, 0 MACs = 0% MACs, 662.09 us = 0.06% latency, 0 FLOPS, p=0.1, inplace=False)
>     )
> 
> # ...clipped...
> 
>           (mlp): ParallelMLP(
>             135.27 M = 5.66% Params, 3.32 TMACs = 5.99% MACs, 35.1 ms = 3.01% latency, 189.4 TFLOPS
>             (dense_h_to_4h): ColumnParallelLinear(90.18 M = 3.78% Params, 2.22 TMACs = 3.99% MACs, 19.31 ms = 1.65% latency, 229.56 TFLOPS)
>             (dense_4h_to_h): RowParallelLinear(45.09 M = 1.89% Params, 1.11 TMACs = 2% MACs, 10.94 ms = 0.94% latency, 202.54 TFLOPS)
>           )
>         )
>       )
>       (final_layernorm): RMSNorm(4.1 K = 0% Params, 0 MACs = 0% MACs, 5.38 ms = 0.46% latency, 0 FLOPS)
>     )
>     (output_layer): ColumnParallelLinear(131.07 M = 5.49% Params, 0 MACs = 0% MACs, 0 s = 0% latency, 0 FLOPS)
>   )
> )
> ------------------------------------------------------------------------------
> [2024-04-19 13:30:54,286] [INFO] [profiler.py:226:end_profile] Flops profiler finished
> [2024-04-19 13:30:54,286] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9340.38 | bwd_microstep: -296010.26 | bwd_inner_microstep: -298701.16 | bwd_allreduce_microstep: 2690.53 | step_microstep: 158.63
> [2024-04-19 13:30:54,286] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 0.00 | bwd: 0.00 | bwd_inner: -298701.19 | bwd_allreduce: 2690.52 | step: 0.00
> [2024-04-19 13:30:54][INFO][training:1251] -  iteration=       5/   10000 | consumed_samples=        5760 | consumed_tokens=    23592960 | elapsed_time_per_iteration_ms=62925.6 | learning_rate=0.000010 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.307 | tokens_per_gpu_per_second_tgs=3124.453 | TFLOPs=72.91 |
> [2024-04-19 13:31:57,082] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 131.51 | optimizer_gradients: 1.72 | optimizer_step: 14.38
> [2024-04-19 13:31:57,082] [INFO] [logging.py:96:log_dist] [Rank 0] step=6, skipped=0, lr=[1.2e-05, 1.2e-05], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:31:57,083] [INFO] [timer.py:260:stop] epoch=0/micro_step=6/global_step=6, RunningAvgSamplesPerSec=152.60343065546638, CurrSamplesPerSec=157.20324398714874, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> [2024-04-19 13:31:57,084] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9227.08 | bwd_microstep: 47662.14 | bwd_inner_microstep: 44982.86 | bwd_allreduce_microstep: 2678.89 | step_microstep: 156.24
> [2024-04-19 13:31:57,084] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9227.00 | bwd: 47662.04 | bwd_inner: 44982.83 | bwd_allreduce: 2678.89 | step: 156.26
> [2024-04-19 13:31:57][INFO][training:1251] -  iteration=       6/   10000 | consumed_samples=        6912 | consumed_tokens=    28311552 | elapsed_time_per_iteration_ms=62797.2 | learning_rate=0.000012 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.345 | tokens_per_gpu_per_second_tgs=3130.841 | TFLOPs=73.06 |
> [2024-04-19 13:33:00,119] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 132.93 | optimizer_gradients: 1.72 | optimizer_step: 14.38
> [2024-04-19 13:33:00,119] [INFO] [logging.py:96:log_dist] [Rank 0] step=7, skipped=0, lr=[1.4e-05, 1.4e-05], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:33:00,120] [INFO] [timer.py:260:stop] epoch=0/micro_step=7/global_step=7, RunningAvgSamplesPerSec=152.34894429019823, CurrSamplesPerSec=151.33943037839882, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> [2024-04-19 13:33:00,120] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9273.43 | bwd_microstep: 47630.66 | bwd_inner_microstep: 44919.22 | bwd_allreduce_microstep: 2711.06 | step_microstep: 157.68
> [2024-04-19 13:33:00,121] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9273.33 | bwd: 47630.56 | bwd_inner: 44919.18 | bwd_allreduce: 2711.05 | step: 157.70
> [2024-04-19 13:33:00][INFO][training:1251] -  iteration=       7/   10000 | consumed_samples=        8064 | consumed_tokens=    33030144 | elapsed_time_per_iteration_ms=63036.9 | learning_rate=0.000014 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.275 | tokens_per_gpu_per_second_tgs=3118.936 | TFLOPs=72.78 |
> [2024-04-19 13:34:03,789] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 127.76 | optimizer_gradients: 1.72 | optimizer_step: 14.27
> [2024-04-19 13:34:03,789] [INFO] [logging.py:96:log_dist] [Rank 0] step=8, skipped=0, lr=[1.6000000000000003e-05, 1.6000000000000003e-05], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2024-04-19 13:34:03,790] [INFO] [timer.py:260:stop] epoch=0/micro_step=8/global_step=8, RunningAvgSamplesPerSec=152.09697211753837, CurrSamplesPerSec=150.8495109293225, MemAllocated=5.56GB, MaxMemAllocated=16.6GB
> [2024-04-19 13:34:03,790] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd_microstep: 9296.92 | bwd_microstep: 47560.25 | bwd_inner_microstep: 44876.50 | bwd_allreduce_microstep: 2683.35 | step_microstep: 151.80
> [2024-04-19 13:34:03,791] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | fwd: 9296.84 | bwd: 47560.15 | bwd_inner: 44876.46 | bwd_allreduce: 2683.35 | step: 151.82
> [2024-04-19 13:34:03][INFO][training:1251] -  iteration=       8/   10000 | consumed_samples=        9216 | consumed_tokens=    37748736 | elapsed_time_per_iteration_ms=63669.6 | learning_rate=0.000016 | global_batch_size= 1152 | loss_scale=1.0 | actual_seqlen= 4096 | number_of_skipped_iterations=  0 | number_of_nan_iterations=  0 | samples_per_second=18.093 | tokens_per_gpu_per_second_tgs=3087.940 | TFLOPs=72.06 |
> ```
>

### 2024-04-16

#### Completed

- [x] Add last weeks' update to [`auroragpt-anl/training`](https://github.com/auroraGPT-ANL/training)
- [x] Added support for [`facebookresearch/schedule_free`](github.com/facebookresearch/schedule_free)
    - via `OPT={adamwschedulefree,sgdschedulefree}`
    - Additional flag for `--schedulefree-foreach`

```python
    foreach (bool): Use a foreach-backed implementation of the optimizer.
                Should be significantly faster, but will have higher peak memory
                usage (default True).
    ```

### 2024-04-03

- [x] Aggregate numbers for total training job of 7B model
- [ ] Write up list of tasks required to finish pre-training

#### Last Weeks Update

1. Updates:
    - **Convergence on XPU**

#### Total Training Time

The total training time, $T$, is the sum of the time taken for each iteration,
$\tau_{i}$, measured in $\left[{\mathrm{seconds}}\, /\, {\mathrm{iteration}}\right]$.

We can get an estimate for the total required training time by taking the
average time per step and multiplying by the total number of training steps

$$
\begin{align}
\textcolor{#36CE5E}{T} \equiv \sum_{i} \tau_{i} &\simeq \left\langle\tau\right \rangle \left[\frac{\mathrm{sec}}{\mathrm{iter}}\right] \times N_{\mathrm{train}} \\

&= \left\langle\tau\right\rangle \left[\frac{\mathrm{sec}}{\mathrm{iter}}\right] \times 320,000 \left[\mathrm{iter}\right] \times \frac{1}{60} \left[\frac{\mathrm{min}}{\mathrm{sec}}\right] \times \frac{1}{60} \left[\frac{\mathrm{hr}}{\mathrm{min}}\right]\times \frac{1}{24}\left[\frac{\mathrm{day}}{\mathrm{hr}}\right] \\

\textcolor{#36CE5E}{T} &\simeq \mathbf{\textcolor{red}{3.7} \times \textcolor{#1a8ffd}{\left\langle\tau\right\rangle}}
\end{align}
$$

where $\langle \tau\rangle$ is the average time per training iteration, measured in seconds.

- \[**Computation**\]: For `X [seconds/iteration]`
    - `total_train_time`: `X [sec/iter] * 320,000 [iter] * (1/60) [sec/min] * (1/60) [min/hr] * (1/24) [day/hr]`
    - `total_train_time`: `X [sec/iter] * 3.703 [iter][sec][day]`
- \[**Polaris**\]
    - throughput: `~ 14 [sec / iteration] @ ~ 70 TFLOPs`
    - total train time:
        - `~ 14 [sec / iter] * 320,000 [iter] * (1 / 60) [sec / min] * (1 / 60) [min / hr] * (1 / 24) [day / hr]`
        - `~ 14 [sec / iter] * 3.703 [iter][sec][day]`
        - `~ 51.852 [day]`
- \[**Sunspot**\]
    - throughput:
        - `base`: `21.45 ± 2.523 (19.235, 23.763) [sec / iteration]`
        - `flash-attn`: `17.46 ± 0.07833 (17.405, 17.516) [sec / iteration]`
    - total train time:
        - `base` : `~ 80 [day]` \[`:= 21.45 [sec / iter] * 3.703 [iter][sec][day]`\]
        - `flash`: `~ 65 [day]` \[`:= 17.46 [sec / iter] * 3.703 [iter][sec][day]`\]

### 2024-04-01

- [ ] Start benchmarking 70B model
- [ ] Need to get `nsys` data from Perlmutter due @ ==2024-04-03==

#### Polaris
- [ ] Need longer training runs **with** and **without** `--use-flash-attn-v2` on Polaris with `OPT=adam`

#### Sunspot
- [ ] Try `MiCS` config on Sunspot
- [ ] Latest version of Dolma dataset \[WIP\]
    - [/] Download in process
    - [ ] Will need to tokenize

# 2024-03
## 2024-03-28

### Weekly Update

- Updates:
    - Working on gathering performance measurements for Llama2-70B architecture on Polaris / Sunspot.
    - Ongoing effort to train full Llama-7B architecture with Dolma dataset on Polaris.
        - We observed that, shortly after the learning rate warmup completes, the loss curve begins to have significant spikes that cause the training procedure to crash with `NaN`.
        - To mitigate this, we've implemented a mechanism for manually skipping the backpropagation update when this happens. If this method works effectively, we will automate it in the training pipeline.
    - Convergence issues on Aurora / Sunspot (PVC)
        - When training with identical configs on Polaris / Sunspot, we observed a disagreement in their loss curves. Specifically, we notice that the loss curve on PVC seems to plateau (as shown in the figure below).
        - Through an exhaustive debugging process, we were able to identify that the issue is resulting from an ambiguity in how Megatron-DeepSpeed creates the internal optimizer states. A method for resolving the issue has been proposed, and ongoing work to verify this is underway.
    - Training on Sunspot
        - In order to make progress while Aurora is unavailable we will continue pre-training on Sunspot. This requires creating (and tokenizing) an additional copy of the Dolma dataset on the `gila` filesystem. This is currently a work in progress.
- Blockers:
    - Jobs on Polaris have been slow to get through the queue due to the upcoming Gordon Bell submission deadline.
    - This has made it difficult to confirm the effectiveness of our "loss spike mitigation" technique, though tests have been ongoing at smaller scales.
    - Full scale pre-training on Sunspot had (previously) been blocked by the apparent convergence issue, and effort was re-focused to try and quickly tackle this issue.
        - We believe this issue has now been identified and a fix proposed. Once Sunspot is back online Monday, we will be able to perform these tests.
- References (links to any meeting notes, files, presentations to support
    - ![intel-convergence#invert](./assets/intel-convergence-issue.png)
- Shoutouts (if you want):

## 2024-03-25

- Polaris:
    - `apex.optimizers.fused_adam.FusedAdam`:
        - WB Run: [glamorous-puddle-818](https://wandb.ai/aurora_gpt/AuroraGPT/runs/jno7708z)
    - `torch.optim.Adam`:
        - WB Run: [trim-donkey-829](https://wandb.ai/aurora_gpt/AuroraGPT/runs/m65khgna)
    - `torch.optim.AdamW`:
        - WB Run: [lucky-dust-830](https://wandb.ai/aurora_gpt/AuroraGPT/runs/ssw888p4)
- Sunspot:
    - `torch.optim.Adam`:
        - WB Run: [azure-totem-827](https://wandb.ai/aurora_gpt/AuroraGPT/runs/ngi5f6c3)
    - `torch.optim.AdamW`:
        - WB Run: [electric-star-831](https://wandb.ai/aurora_gpt/AuroraGPT/runs/9ixn0i0c)

### Convergence on Sunspot

    - Earlier:
        - Sunspot:
            - `[2024-03-25 15:56:48,539] [INFO] [utils.py:56:is_zero_supported_optimizer] Checking ZeRO support for optimizer=Adam type=<class 'torch.optim.adam.Adam'>`
                - W&B Run: [likely-donkey-814](https://wandb.ai/aurora_gpt/AuroraGPT/runs/hj53w0fo?nw=nwuserforemans)
        - Polaris:
            - `[2024-03-25 15:58:27,034] [INFO] [utils.py:56:is_zero_supported_optimizer] Checking ZeRO support for optimizer=FusedAdam type=<class 'apex.optimizers.fused_adam.FusedAdam'>`
                - W&B Run: [logical-capybara-815](https://wandb.ai/aurora_gpt/AuroraGPT/runs/x834b0fz?nw=nwuserforemans)

- `dolma` on Sunspot?
- Restarting production training on Polaris
    - `--train-iters-to-skip` for "skipping" bad data

## 2024-03-22

### Convergence Issue \[Update\]

> [!success]+ Llama Convergence
>
> From Deepak:
>
> Hi Sam/Venkat,
>
> I have been looking into the optimizer issue, and I think that the delta we are seeing between PVC and Polaris comes down to default behavior of the optimizers.
>
> We want to run with AdamW , but the Megatron-DS code accepts only Adam/SGD.
> The optimizer is created in Megatron and passed to DS init function – this is a bug that we need to fix. Please see output below and same should be happening for Lamb as well.
>
> ```bash
> (base) drcanchi@uan-0001:~/alcf-megatronDS> grep adam run_llama.sh.o8269183
> cpu_adam ............... [NO] ....... [OKAY]
> fused_adam ............. [NO] ....... [OKAY]
>   adam_beta1 ...................................... 0.9
>   adam_beta2 ...................................... 0.999
>   adam_eps ........................................ 1e-08
>   cpu_torch_adam .................................. False
>   ds_fused_adam ................................... False
>   optimizer ....................................... adam
> cpu_adam ............... [NO] ....... [OKAY]
> fused_adam ............. [NO] ....... [OKAY]
> [2024-03-15 00:22:02,987] [INFO] [utils.py:56:is_zero_supported_optimizer] Checking ZeRO support for optimizer=Adam type=<class 'torch.optim.adam.Adam'>
> [2024-03-15 00:22:12,619] [INFO] [config.py:988:print]   optimizer_name ............... adamw
> ```
>
> The interesting part here is that the Fused Adam in APEX, DS CPU and DS XPU all have an option to set AdamW mode and it defaults to True – so DS CPU and Polaris Adam are actually running AdamW while PVC path is doing Adam. Note that Adam and AdamW are separate optimizers in Pytorch. By changing to AdamW, we can reproduce the loss curve  of DS CPU and DS XPU optimizers.
>
> ![#invert](assets/ScreenShot-2024-03-22-125519.png){.center}
>
> To validate this hypothesis, we should run APEX Fused Adam with AdamW mode disabled or just use torch Adam on Polaris. The expectation is it should behave like what we were seeing on Sunspot. Note that above data is without Flash – higher loss with Flash is still being investigated.
>
> Thanks
> Deepak

## 2024-03-19

### `TFLOPs` vs `GAS`

- Constant across runs:
```yaml
    world_size: 32
    micro_batch: 8
    NLAYERS: 32
    TP: 2
    use_flash_attn: true
    ```

| TFLOPS  | GAS | GBS  | DTYPE |
| :-----: | :-: | :--: | :---: |
| 102.869 |  8  | 1024 | bf16  |
| 92.445  |  4  | 512  | bf16  |
| 84.721  |  2  | 256  | bf16  |
| 83.211  |  1  | 128  | fp16  |
| 77.095  |  1  | 128  | bf16  |
| 75.954  |  1  | 128  | fp16  |

## 2024-03-13

Summary to Rick:

Here are some updates on the status here.

> The group here, Sam Foreman, Varuni Sastry, Huihuo Zheng, Murali Emani) has put in quite a lot of effort.
>
> We do have one key issue to resolve (more below)
>
> 1. Megatron-Deepspeed data-processing pipelines have been completely overhauled.
>
>     We found and fixed several issues in Megatron-Deepspeed's implementation to process the entire Dolma data set.
>
>     We had to rewrite and overhaul quite a bit here.
>
> 	- This includes solving issues how Megaton handles the large number of datasets(files), sampling across corpora, processing of the data, etc.
>
> 	    We have validated that the Dolma datasets are processed, including at scale, and sampled based on the weights we need now across the corpora.
>
> 	    We have also built several utilities for validation here.
>
> 3. Several issues in the model implementation in Megatron-Deepseed's resolved.
> We have been fixing issues with the implementation here as we encounter them at
> various scales.
>
> 3. We are able to run on Aurora and Polaris with the software stack and training
> on Dolma. We have lots of performance data here and will summarize these.
>
> 4. We have the Polaris training run ongoing and execute this to completion.
>

# 2024-02
## 2024-02-12

- [ ] Kick-start training runs
- [ ] Look at `MICS` settings

- [ ] Continue training on Polaris

## 2024-02-07

- [ ] Try with `Megatron-LM` data-pre-processing pipeline to see if that works
- [ ] Try with `--data_impl mmap` instead of `--data_impl infer`
- [ ] Take subset (say half) of DOLMA with same relative distributions
    - [ ] Run on that entire dataset, train, save checkpoint
    - [ ] Load from that checkpoint, restart training with OTHER half of DOLMA
    - [ ] To no bias training, need to ensure relative distributions consistent across DOLMA splits
- [ ] Look at `--lr-decay` related parameters
- [ ] Parallelize the index creation

- Distribute index building in data pre-processing pipeline
- Aggregate metadata about each workers "seen" files on RANK 0 to coordinate global indexing

## Intel Meeting

- [ ] Try with `ZERO_STAGE=3` and NO [`flash-attn`](`flash-attn`.md)
- [ ] Try with `ZERO_STAGE=2` and `--use-flash-attn{-v2}`

## 2024-02-05

- [ ] Start training run with Megatron-DeepSpeed

- [ ] Finalize hyperparameters
    - [ ] `ZERO_STAGE=2`
    - [ ] `MICRO_BATCH=8`
    - [ ] `TP=2`
    - [ ] `NUM_NODES=64`
    - [ ] `GRAD_ACC_STEPS=1`
    - [ ] `--use-flash-attn-v2`
    - [ ] `SEQ_LEN=4096`

- [ ] How to restore from checkpoint with different `DATA_PARALLEL_SIZE` ?
    - [ ] Checkpointing / restarting with different `WORLD_SIZE` in general
    - [ ] Get a better understanding of checkpointing / restoring logic in general

- [ ] Murali able to fix profiling issues by writing to unique file on each rank

- [x] Try with `--use-flash-attn` on single node of Aurora
- [x] Try with `PP > 1` and `--normalization rmsnorm` on Polaris to see if this works
    - [x] 🚀 [celestial-plianet-1015](https://wandb.ai/l2hmc-qcd/GenSLM-Megatron-DS/runs/knzwfov3)
```bash
    $ [...] --pipeline-model-parallel-size 2 --normalization rmsnorm
    ```

- [ ] Try with `ZERO_STAGE=3`, `MICS_shard_size=8` and `TP=1`
    - [reference](https://github.com/microsoft/DeepSpeed/blob/24f20ef0a105d32f6085fe0d3b1c2f9324a6262c/deepspeed/runtime/zero/mics.py#L328)

## 2024-02-02

- [ ] Working on 🦙 Llama 2 Notebook with 🤗 Transformers
- [ ] Try with `MICS=8` on Polaris
- [ ] Checkpoint every 100 iterations
    - Async checkpointing, write
    - how should we checkpoint for 70B model
        - sharded weights -> will need to aggregate before saving checkpoint
- [ ] Mechanism for detecting spikes
- [x] disable `activation_checkpointing` and see what performance we get
    - [x] 🚀 [summer-blaze-1016](https://wandb.ai/l2hmc-qcd/GenSLM-Megatron-DS/runs/a1plynuq?workspace=user-saforem2) (same as `celestial-planet-1015` below, but with `USE_ACTIVATION_CHECKPOINTING=0`)
- [x] Try with `PP > 1` and `--rms-norm` flag and see if this works on Polaris
    - [x] 🚀 [celestial-planet-1015](https://wandb.ai/l2hmc-qcd/GenSLM-Megatron-DS/runs/knzwfov3)
```bash
    $ [...] --pipeline-model-parallel-size 2 [...] --normalization rmsnorm
    ```
- [ ] Figure out `MiCS` config ??
- [ ] [MiCS implementation #2964](https://github.com/microsoft/DeepSpeed/pull/2964)
- [ ] Invite Minjia to ongoing DeepSpeed meetings ???? **Minjia's personal email** : zhangninja@gmail.com

## 2024-02-01

### Intel Call

- [ ] Try with `ZERO_STAGE=3` `MICS_shard_size=8` and `TP=1`
    - [ ] [reference](https://github.com/microsoft/DeepSpeed/blob/24f20ef0a105d32f6085fe0d3b1c2f9324a6262c/deepspeed/runtime/zero/mics.py#L328)
- [ ] Can increase `mics_shard_size` and see if this improves throughput
- [ ] Increase `mics_shard_size` reduces memory pressure (might work with disabling activation checkpointing)

- [ ] Grouped query attention
- [ ] Activation checkpointing ?
    - [ ] will need robust checkpointing mechanism
    - [ ] Should aim to disable `activation_checkpointing` if possible
        - [ ] WIll need robust checkpointing / restoring mechanism
    - [ ] Might be possible with `PP > 1`
- [ ] Work on developing performance model to predict / anticipate how settings will impact performance when going from 7b -> 70b model
- [ ] Better understand what performance gains to be expected through different options / settings

### Flash Attention

- [ ] Will take a long time to compile on first attempt
- [ ] `--use-flash-attn`

### Polaris

- [ ] Try `ZeRO=3` with TP=1
- [ ] Try with increasing `MICS=8`
- [ ] Try adding group query

- [ ] `PP > 1`
- [ ] Start working on checkpoint + restoring mechanmism
- [ ] Using current `candidate` config, try again on `{Polaris, Perlmutter}` and measure computation / communication overlap using `nSys`