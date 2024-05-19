```Shell
/bin/bash: /lus/grand/projects/datascience/foremans/locations/thetaGPU/miniconda3/envs/2022-07-01/lib/libtinfo.so.6: no version information available (required by /bin/bash)
cwd: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof
parent: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src
ROOT: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof
Job started at: 2023-01-11-132641
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
┃  RUNNING ON thetaGPU: 32 GPUs
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DIR=/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof
PARENT=/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src
ROOT=/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof
LOGDIR=/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs
LOGFILE=/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs/2023-01-11-132641-thetagpu12_ngpu32.log
Found venv at: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
┃  STARTING A NEW RUN ON 32 GPUs of thetaGPU
┃━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
┃  - Writing logs to: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs/2023-01-11-132641-thetagpu12_ngpu32.log
┃  - DATE: 2023-01-11-132641
┃  - NRANKS: 4
┃  - NGPUS PER RANK: 8
┃  - NGPUS TOTAL: 32
┃  - python3: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/bin/python3
┃  - MPI: /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpirun
┃  - exec: /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpirun -x LD_LIBRARY_PATH     -x PATH     -n 32     -npernode 8     --hostfile /var/tmp/cobalt.10121193 /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/bin/python3 /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/main.py backend=deepspeed
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
To view output: `tail -f $(tail -1 logs/latest)`
Latest logfile: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs/2023-01-11-132641-thetagpu12_ngpu32.log
tail -f /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs/2023-01-11-132641-thetagpu12_ngpu32.log
/bin/bash: /lus/grand/projects/datascience/foremans/locations/thetaGPU/miniconda3/envs/2022-07-01/lib/libtinfo.so.6: no version information available (required by /bin/bash)
wandb: Currently logged in as: saforem2 (l2hmc-qcd). Use `wandb login --relogin` to force relogin
wandb: wandb version 0.13.8 is available!  To upgrade, please run:
wandb:  $ pip install wandb --upgrade
wandb: Tracking run with wandb version 0.13.7
wandb: Run data is saved locally in /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/outputs/2023-01-11/13-26-55/wandb/run-20230111_132659-w583f6br
wandb: Run `wandb offline` to turn off syncing.
wandb: Syncing run olive-silence-244
wandb: ⭐️ View project at https://wandb.ai/l2hmc-qcd/mlprof
wandb: 🚀 View run at https://wandb.ai/l2hmc-qcd/mlprof/runs/w583f6br
```

- `cat /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/logs/2023-01-11-132641-thetagpu12_ngpu32.log`:
> [!INFO] `cat $(tail -1 logs/latest)`
> ```Shell
> [2023-01-11 13:26:55,662] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,663] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,663] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,663] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,664] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,664] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,665] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,665] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,673] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,775] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,775] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,776] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,776] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,777] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,777] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,777] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,799] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,804] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,805] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,822] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,823] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,885] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,887] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,888] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,890] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,890][mlprof.utils.dist][INFO] - Using deepspeed for distributed training
> [2023-01-11 13:26:55,891] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,894] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,895] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,896] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,896] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,896] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,897] [INFO] [comm.py:638:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=6, local_rank=6, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=2, local_rank=2, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=5, local_rank=5, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=4, local_rank=4, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=3, local_rank=3, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=1, local_rank=1, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=7, local_rank=7, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=8, local_rank=0, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=0, local_rank=0, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=18, local_rank=2, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=10, local_rank=2, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,977] [INFO] [comm.py:654:init_distributed] Initializing TorchBackend in DeepSpeed with backend nccl
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=14, local_rank=6, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=23, local_rank=7, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=12, local_rank=4, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=15, local_rank=7, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=16, local_rank=0, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=11, local_rank=3, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=9, local_rank=1, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=13, local_rank=5, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=28, local_rank=4, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=20, local_rank=4, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=22, local_rank=6, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=19, local_rank=3, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=30, local_rank=6, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=21, local_rank=5, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=27, local_rank=3, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=31, local_rank=7, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=24, local_rank=0, world_size=32, master_addr=10.230.2.200, master_port=29500
> [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=26, local_rank=2, world_size=32, master_addr=10.230.2.200, master_port=29500
>     [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=29, local_rank=5, world_size=32, master_addr=10.230.2.200, master_port=29500
>     [2023-01-11 13:26:55,976] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=25, local_rank=1, world_size=32, master_addr=10.230.2.200, master_port=29500
>     [2023-01-11 13:26:55,978] [INFO] [comm.py:690:mpi_discovery] Discovered MPI settings of world_rank=17, local_rank=1, world_size=32, master_addr=10.230.2.200, master_port=29500
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 23
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 30
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 20
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 14
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 31
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 26
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 25
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 27
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 11
>     [2023-01-11 13:26:56,010][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 22
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 29
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 13
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 21
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 19
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 16
>     [2023-01-11 13:26:56,011][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 17
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 6
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 4
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 7
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 2
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 5
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 3
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 1
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 18
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 8
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 24
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 12
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 9
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 10
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 28
>     [2023-01-11 13:26:56,978][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 15
>     [2023-01-11 13:26:56,987][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:1 to store for rank: 0
>     [2023-01-11 13:26:56,988][torch.distributed.distributed_c10d][INFO] - Rank 14: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,988][torch.distributed.distributed_c10d][INFO] - Rank 21: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,989][torch.distributed.distributed_c10d][INFO] - Rank 26: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,990][torch.distributed.distributed_c10d][INFO] - Rank 31: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,991][torch.distributed.distributed_c10d][INFO] - Rank 16: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,991][torch.distributed.distributed_c10d][INFO] - Rank 22: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,991][torch.distributed.distributed_c10d][INFO] - Rank 23: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,992][torch.distributed.distributed_c10d][INFO] - Rank 27: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,992][torch.distributed.distributed_c10d][INFO] - Rank 11: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,992][torch.distributed.distributed_c10d][INFO] - Rank 17: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,993][torch.distributed.distributed_c10d][INFO] - Rank 25: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,993][torch.distributed.distributed_c10d][INFO] - Rank 29: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,996][torch.distributed.distributed_c10d][INFO] - Rank 13: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,996][torch.distributed.distributed_c10d][INFO] - Rank 19: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,996][torch.distributed.distributed_c10d][INFO] - Rank 30: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,996][torch.distributed.distributed_c10d][INFO] - Rank 20: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:56,998][torch.distributed.distributed_c10d][INFO] - Rank 6: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,000][torch.distributed.distributed_c10d][INFO] - Rank 18: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,002][torch.distributed.distributed_c10d][INFO] - Rank 24: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,003][torch.distributed.distributed_c10d][INFO] - Rank 8: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,005][torch.distributed.distributed_c10d][INFO] - Rank 4: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,007][torch.distributed.distributed_c10d][INFO] - Rank 28: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,009][torch.distributed.distributed_c10d][INFO] - Rank 12: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,010][torch.distributed.distributed_c10d][INFO] - Rank 7: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,015][torch.distributed.distributed_c10d][INFO] - Rank 15: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,016][torch.distributed.distributed_c10d][INFO] - Rank 2: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,021][mlprof.utils.dist][INFO] - Global Rank: 21 / 31
>     [2023-01-11 13:26:57,021][torch.distributed.distributed_c10d][INFO] - Rank 10: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,022][torch.distributed.distributed_c10d][INFO] - Rank 5: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,026][torch.distributed.distributed_c10d][INFO] - Rank 9: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,027][torch.distributed.distributed_c10d][INFO] - Rank 3: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,032][torch.distributed.distributed_c10d][INFO] - Rank 1: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,035][mlprof.utils.dist][INFO] - Global Rank: 26 / 31
>     [2023-01-11 13:26:57,042][mlprof.utils.dist][INFO] - Global Rank: 22 / 31
>     [2023-01-11 13:26:57,045][mlprof.utils.dist][INFO] - Global Rank: 14 / 31
>     [2023-01-11 13:26:57,050][mlprof.utils.dist][INFO] - Global Rank: 11 / 31
>     [2023-01-11 13:26:57,054][mlprof.utils.dist][INFO] - Global Rank: 31 / 31
>     [2023-01-11 13:26:57,055][mlprof.utils.dist][INFO] - Global Rank: 16 / 31
>     [2023-01-11 13:26:57,062][mlprof.utils.dist][INFO] - Global Rank: 27 / 31
>     [2023-01-11 13:26:57,065][mlprof.utils.dist][INFO] - Global Rank: 23 / 31
>     [2023-01-11 13:26:57,065][mlprof.utils.dist][INFO] - Global Rank: 25 / 31
>     [2023-01-11 13:26:57,066][mlprof.utils.dist][INFO] - Global Rank: 29 / 31
>     [2023-01-11 13:26:57,069][mlprof.utils.dist][INFO] - Global Rank: 17 / 31
>     [2023-01-11 13:26:57,071][mlprof.utils.dist][INFO] - Global Rank: 19 / 31
>     [2023-01-11 13:26:57,074][torch.distributed.distributed_c10d][INFO] - Rank 0: Completed store-based barrier for key:store_based_barrier_key:1 with 32 nodes.
>     [2023-01-11 13:26:57,101][mlprof.utils.dist][INFO] - [21]: Local rank: 5
>     [2023-01-11 13:26:57,106][mlprof.utils.dist][INFO] - [22]: Local rank: 6
>     [2023-01-11 13:26:57,108][mlprof.utils.dist][INFO] - [26]: Local rank: 2
>     [2023-01-11 13:26:57,112][mlprof.utils.dist][INFO] - [16]: Local rank: 0
>     [2023-01-11 13:26:57,112][mlprof.utils.dist][INFO] - Global Rank: 6 / 31
>     [2023-01-11 13:26:57,113][mlprof.utils.dist][INFO] - [31]: Local rank: 7
>     [2023-01-11 13:26:57,113][mlprof.utils.dist][INFO] - Global Rank: 30 / 31
>     [2023-01-11 13:26:57,116][mlprof.utils.dist][INFO] - Global Rank: 13 / 31
>     [2023-01-11 13:26:57,117][mlprof.utils.dist][INFO] - Global Rank: 20 / 31
>     [2023-01-11 13:26:57,117][mlprof.utils.dist][INFO] - [23]: Local rank: 7
>     [2023-01-11 13:26:57,118][mlprof.utils.dist][INFO] - [27]: Local rank: 3
>     [2023-01-11 13:26:57,121][mlprof.utils.dist][INFO] - Global Rank: 18 / 31
>     [2023-01-11 13:26:57,122][mlprof.utils.dist][INFO] - [17]: Local rank: 1
>     [2023-01-11 13:26:57,124][mlprof.utils.dist][INFO] - [25]: Local rank: 1
>     [2023-01-11 13:26:57,125][mlprof.utils.dist][INFO] - [14]: Local rank: 6
>     [2023-01-11 13:26:57,125][mlprof.utils.dist][INFO] - Global Rank: 24 / 31
>     [2023-01-11 13:26:57,126][mlprof.utils.dist][INFO] - Global Rank: 28 / 31
>     [2023-01-11 13:26:57,128][mlprof.utils.dist][INFO] - [19]: Local rank: 3
>     [2023-01-11 13:26:57,129][mlprof.utils.dist][INFO] - [29]: Local rank: 5
>     [2023-01-11 13:26:57,130][mlprof.utils.dist][INFO] - [11]: Local rank: 3
>     [2023-01-11 13:26:57,135][mlprof.utils.dist][INFO] - [13]: Local rank: 5
>     [2023-01-11 13:26:57,136][mlprof.utils.dist][INFO] - Global Rank: 4 / 31
>     [2023-01-11 13:26:57,136][mlprof.utils.dist][INFO] - [6]: Local rank: 6
>     [2023-01-11 13:26:57,138][mlprof.utils.dist][INFO] - Global Rank: 8 / 31
>     [2023-01-11 13:26:57,142][mlprof.utils.dist][INFO] - [4]: Local rank: 4
>     [2023-01-11 13:26:57,145][mlprof.utils.dist][INFO] - [30]: Local rank: 6
>     [2023-01-11 13:26:57,147][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,147][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,148][mlprof.utils.dist][INFO] - Global Rank: 12 / 31
>     [2023-01-11 13:26:57,148][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,149][mlprof.utils.dist][INFO] - [20]: Local rank: 4
>     [2023-01-11 13:26:57,150][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,151][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,151][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,153][mlprof.utils.dist][INFO] - Global Rank: 7 / 31
>     [2023-01-11 13:26:57,153][mlprof.utils.dist][INFO] - Global Rank: 15 / 31
>     [2023-01-11 13:26:57,156][mlprof.utils.dist][INFO] - Global Rank: 10 / 31
>     [2023-01-11 13:26:57,156][mlprof.utils.dist][INFO] - [8]: Local rank: 0
>     [2023-01-11 13:26:57,157][mlprof.utils.dist][INFO] - Global Rank: 9 / 31
>     [2023-01-11 13:26:57,163][mlprof.utils.dist][INFO] - Global Rank: 2 / 31
>     [2023-01-11 13:26:57,169][mlprof.utils.dist][INFO] - Global Rank: 5 / 31
>     [2023-01-11 13:26:57,173][mlprof.utils.dist][INFO] - Global Rank: 3 / 31
>     [2023-01-11 13:26:57,176][mlprof.utils.dist][INFO] - Global Rank: 0 / 31
>     [2023-01-11 13:26:57,257][mlprof.utils.dist][INFO] - [0]: Local rank: 0
>     [2023-01-11 13:26:57,226][mlprof.utils.dist][INFO] - [5]: Local rank: 5
>     [2023-01-11 13:26:57,175][mlprof.utils.dist][INFO] - Global Rank: 1 / 31
>     [2023-01-11 13:26:57,252][mlprof.utils.dist][INFO] - [1]: Local rank: 1
>     [2023-01-11 13:26:57,177][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,177][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,247][mlprof.utils.dist][INFO] - [3]: Local rank: 3
>     [2023-01-11 13:26:57,188][mlprof.utils.dist][INFO] - [7]: Local rank: 7
>     [2023-01-11 13:26:57,281][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,194][mlprof.utils.dist][INFO] - [2]: Local rank: 2
>     [2023-01-11 13:26:57,176][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,176][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,177][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,177][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,190][mlprof.utils.dist][INFO] - [18]: Local rank: 2
>     [2023-01-11 13:26:57,177][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,192][mlprof.utils.dist][INFO] - [24]: Local rank: 0
>     [2023-01-11 13:26:57,203][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,193][mlprof.utils.dist][INFO] - [12]: Local rank: 4
>     [2023-01-11 13:26:57,197][mlprof.utils.dist][INFO] - [28]: Local rank: 4
>     [2023-01-11 13:26:57,250][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,246][mlprof.utils.dist][INFO] - [15]: Local rank: 7
>     [2023-01-11 13:26:57,253][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,261][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,251][mlprof.utils.dist][INFO] - [10]: Local rank: 2
>     [2023-01-11 13:26:57,257][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,281][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,261][mlprof.utils.dist][INFO] - [9]: Local rank: 1
>     [2023-01-11 13:26:57,263][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,283][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,285][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,286][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,288][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,290][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,294][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,297][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,300][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,301][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,303][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:26:57,311][mlprof.configs][WARNING] - Loading DeepSpeed config from: /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/src/mlprof/conf/ds_config.json
>     [2023-01-11 13:27:00,749] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:00,750][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 14
>     [2023-01-11 13:27:00,895] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:00,897][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 4
>     [2023-01-11 13:27:00,960] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:00,961][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 13
>     [2023-01-11 13:27:00,975] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:00,976][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 6
>     [2023-01-11 13:27:01,060] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,061][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 9
>     [2023-01-11 13:27:01,062] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,063][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 26
>     [2023-01-11 13:27:01,068] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,070][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 18
>     [2023-01-11 13:27:01,106] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,108][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 25
>     [2023-01-11 13:27:01,114] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,115] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,116][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 19
>     [2023-01-11 13:27:01,116][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 17
>     [2023-01-11 13:27:01,122] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,123] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,123][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 16
>     [2023-01-11 13:27:01,124][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 21
>     [2023-01-11 13:27:01,125] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,126][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 11
>     [2023-01-11 13:27:01,127] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,127] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,128][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 20
>     [2023-01-11 13:27:01,128] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,129][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 22
>     [2023-01-11 13:27:01,129][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 23
>     [2023-01-11 13:27:01,131] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,132][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 12
>     [2023-01-11 13:27:01,135] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,136] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,137][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 8
>     [2023-01-11 13:27:01,137][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 10
>     [2023-01-11 13:27:01,138] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,139][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 15
>     [2023-01-11 13:27:01,142] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,143] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,144][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 7
>     [2023-01-11 13:27:01,145][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 5
>     [2023-01-11 13:27:01,145] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,147][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 3
>     [2023-01-11 13:27:01,148] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,149][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 2
>     [2023-01-11 13:27:01,155] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,156][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 1
>     [2023-01-11 13:27:01,179] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,180][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 27
>     [2023-01-11 13:27:01,181] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,182][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 29
>     [2023-01-11 13:27:01,200] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,202][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 30
>     [2023-01-11 13:27:01,215] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,216][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 24
>     [2023-01-11 13:27:01,217] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,219][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 28
>     [2023-01-11 13:27:01,228] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:01,230][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 31
>     [2023-01-11 13:27:03,048][mlprof.trainers.pytorch.trainer][WARNING] - Caught wandb.run from: 0
>     {
>       "train_batch_size": 256,
>       "steps_per_print": 5,
>       "optimizer": {
>         "type": "Adam",
>         "params": {
>           "lr": 0.001,
>           "betas": [
>             0.8,
>             0.999
>           ],
>           "eps": 1e-08,
>           "weight_decay": 3e-07
>         }
>       },
>       "scheduler": {
>         "type": "WarmupLR",
>         "params": {
>           "warmup_min_lr": 0,
>           "warmup_max_lr": 0.001,
>           "warmup_num_steps": 1000
>         }
>       },
>       "gradient_clipping": 1.0,
>       "prescale_gradients": false,
>       "fp16": {
>         "enabled": false,
>         "fp16_master_weights_and_grads": false,
>         "loss_scale": 0,
>         "loss_scale_window": 500,
>         "hysteresis": 2,
>         "min_loss_scale": 1,
>         "initial_scale_power": 15
>       },
>       "wall_clock_breakdown": true,
>       "zero_optimization": {
>         "stage": 0,
>         "allgather_partitions": true,
>         "reduce_scatter": true,
>         "allgather_bucket_size": 50000000,
>         "reduce_bucket_size": 50000000,
>         "overlap_comm": true,
>         "contiguous_gradients": true,
>         "cpu_offload": false
>       },
>       "comms_logger": {
>         "enabled": true,
>         "verbose": true,
>         "prof_all": true,
>         "debug": true
>       }
>     }
>     [2023-01-11 13:27:03,068] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed info: version=0.7.7, git-hash=unknown, git-branch=unknown
>     [2023-01-11 13:27:03,068] [WARNING] [config_utils.py:67:_process_deprecated_field] Config parameter cpu_offload is deprecated use offload_optimizer instead
>     [2023-01-11 13:27:03,070][torch.distributed.distributed_c10d][INFO] - Added key: store_based_barrier_key:2 to store for rank: 0
>     [2023-01-11 13:27:03,070][torch.distributed.distributed_c10d][INFO] - Rank 0: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 8: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 13: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 6: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 28: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 26: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 15: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 31: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,072][torch.distributed.distributed_c10d][INFO] - Rank 29: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,071][torch.distributed.distributed_c10d][INFO] - Rank 10: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,072][torch.distributed.distributed_c10d][INFO] - Rank 11: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,072][torch.distributed.distributed_c10d][INFO] - Rank 14: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,073][torch.distributed.distributed_c10d][INFO] - Rank 21: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,073][torch.distributed.distributed_c10d][INFO] - Rank 16: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,073][torch.distributed.distributed_c10d][INFO] - Rank 18: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,074][torch.distributed.distributed_c10d][INFO] - Rank 4: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,074][torch.distributed.distributed_c10d][INFO] - Rank 30: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,075][torch.distributed.distributed_c10d][INFO] - Rank 27: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,077][torch.distributed.distributed_c10d][INFO] - Rank 19: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,077][torch.distributed.distributed_c10d][INFO] - Rank 17: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,077][torch.distributed.distributed_c10d][INFO] - Rank 5: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,077][torch.distributed.distributed_c10d][INFO] - Rank 7: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,077][torch.distributed.distributed_c10d][INFO] - Rank 23: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,078][torch.distributed.distributed_c10d][INFO] - Rank 1: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,078][torch.distributed.distributed_c10d][INFO] - Rank 3: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,078][torch.distributed.distributed_c10d][INFO] - Rank 22: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,078][torch.distributed.distributed_c10d][INFO] - Rank 20: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,078][torch.distributed.distributed_c10d][INFO] - Rank 12: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,079][torch.distributed.distributed_c10d][INFO] - Rank 9: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,079][torch.distributed.distributed_c10d][INFO] - Rank 24: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,079][torch.distributed.distributed_c10d][INFO] - Rank 2: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:03,080][torch.distributed.distributed_c10d][INFO] - Rank 25: Completed store-based barrier for key:store_based_barrier_key:2 with 32 nodes.
>     [2023-01-11 13:27:07,209] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 4138.40 | msg size: 1.12 KB | algbw (Gbps): 0.00  | busbw (Gbps): 0.00
>     [2023-01-11 13:27:07,210] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.13 | msg size: 128.0 B | algbw (Gbps): 0.01  | busbw (Gbps): 0.01
>     [2023-01-11 13:27:07,211] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.10 | msg size: 72.0 KB | algbw (Gbps): 5.96  | busbw (Gbps): 5.96
>     [2023-01-11 13:27:07,211] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.09 | msg size: 256.0 B | algbw (Gbps): 0.02  | busbw (Gbps): 0.02
>     [2023-01-11 13:27:07,211] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.16 | msg size: 576.0 KB | algbw (Gbps): 28.76  | busbw (Gbps): 28.76
>     [2023-01-11 13:27:07,212] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.09 | msg size: 64.0 B | algbw (Gbps): 0.01  | busbw (Gbps): 0.01
>     [2023-01-11 13:27:07,212] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.09 | msg size: 640.0 B | algbw (Gbps): 0.06  | busbw (Gbps): 0.06
>     [2023-01-11 13:27:07,213] [INFO] [logging.py:68:log_dist] [Rank 0] rank=0 | comm op: broadcast | [Caller Func: _broadcast_model] | time (ms): 0.08 | msg size: 40.0 B | algbw (Gbps): 0.00  | busbw (Gbps): 0.00
>     [2023-01-11 13:27:07,213] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed Flops Profiler Enabled: False
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Detected CUDA files, patching ldflags
>     Emitting ninja build file /home/foremans/.cache/torch_extensions/py38_cu114/fused_adam/build.ninja...
>     Building extension module fused_adam...
>     Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     [1/3] /usr/local/cuda-11.4/bin/nvcc  -ccbin /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpicc -DTORCH_EXTENSION_NAME=fused_adam -DTORCH_API_INCLUDE_EXTENSION_H -DPYBIND11_COMPILER_TYPE=\"_gcc\" -DPYBIND11_STDLIB=\"_libstdcpp\" -DPYBIND11_BUILD_ABI=\"_cxxabi1013\" -I/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/includes -I/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/adam -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/torch/csrc/api/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/TH -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/THC -isystem /usr/local/cuda-11.4/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/include/python3.8 -D_GLIBCXX_USE_CXX11_ABI=1 -D__CUDA_NO_HALF_OPERATORS__ -D__CUDA_NO_HALF_CONVERSIONS__ -D__CUDA_NO_BFLOAT16_CONVERSIONS__ -D__CUDA_NO_HALF2_OPERATORS__ --expt-relaxed-constexpr -gencode=arch=compute_80,code=compute_80 -gencode=arch=compute_80,code=sm_80 --compiler-options '-fPIC' -O3 -DVERSION_GE_1_1 -DVERSION_GE_1_3 -DVERSION_GE_1_5 -lineinfo --use_fast_math -gencode=arch=compute_80,code=sm_80 -gencode=arch=compute_80,code=compute_80 -std=c++14 -c /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/adam/multi_tensor_adam.cu -o multi_tensor_adam.cuda.o
>     [2/3] /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpicxx -MMD -MF fused_adam_frontend.o.d -DTORCH_EXTENSION_NAME=fused_adam -DTORCH_API_INCLUDE_EXTENSION_H -DPYBIND11_COMPILER_TYPE=\"_gcc\" -DPYBIND11_STDLIB=\"_libstdcpp\" -DPYBIND11_BUILD_ABI=\"_cxxabi1013\" -I/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/includes -I/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/adam -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/torch/csrc/api/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/TH -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/THC -isystem /usr/local/cuda-11.4/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/include/python3.8 -D_GLIBCXX_USE_CXX11_ABI=1 -fPIC -std=c++14 -O3 -std=c++14 -g -Wno-reorder -DVERSION_GE_1_1 -DVERSION_GE_1_3 -DVERSION_GE_1_5 -c /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/adam/fused_adam_frontend.cpp -o fused_adam_frontend.o
>     [3/3] /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpicxx fused_adam_frontend.o multi_tensor_adam.cuda.o -shared -L/lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/lib -lc10 -lc10_cuda -ltorch_cpu -ltorch_cuda -ltorch -ltorch_python -L/usr/local/cuda-11.4/lib64 -lcudart -o fused_adam.so
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.29804468154907 seconds
>     [2023-01-11 13:27:59,211] [INFO] [logging.py:68:log_dist] [Rank 0] Using DeepSpeed Optimizer param name adam as basic optimizer
>     [2023-01-11 13:27:59,212] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed Basic Optimizer = FusedAdam
>     [2023-01-11 13:27:59,212] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed Final Optimizer = adam
>     [2023-01-11 13:27:59,212] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed using configured LR scheduler = WarmupLR
>     [2023-01-11 13:27:59,212] [INFO] [logging.py:68:log_dist] [Rank 0] DeepSpeed LR Scheduler = <deepspeed.runtime.lr_schedules.WarmupLR object at 0x7f32a7276700>
>     [2023-01-11 13:27:59,212] [INFO] [logging.py:68:log_dist] [Rank 0] step=0, skipped=0, lr=[0.001], mom=[[0.8, 0.999]]
>     [2023-01-11 13:27:59,212] [INFO] [config.py:1020:print] DeepSpeedEngine configuration:
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   activation_checkpointing_config  {
>         "partition_activations": false,
>         "contiguous_memory_optimization": false,
>         "cpu_checkpointing": false,
>         "number_checkpoints": null,
>         "synchronize_checkpoint_boundary": false,
>         "profile": false
>     }
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   aio_config ................... {'block_size': 1048576, 'queue_depth': 8, 'thread_count': 1, 'single_submit': False, 'overlap_events': True}
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   amp_enabled .................. False
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   amp_params ................... False
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   autotuning_config ............ {
>         "enabled": false,
>         "start_step": null,
>         "end_step": null,
>         "metric_path": null,
>         "arg_mappings": null,
>         "metric": "throughput",
>         "model_info": null,
>         "results_dir": "autotuning_results",
>         "exps_dir": "autotuning_exps",
>         "overwrite": true,
>         "fast": true,
>         "start_profile_step": 3,
>         "end_profile_step": 5,
>         "tuner_type": "gridsearch",
>         "tuner_early_stopping": 5,
>         "tuner_num_trials": 50,
>         "model_info_path": null,
>         "mp_size": 1,
>         "max_train_batch_size": null,
>         "min_train_batch_size": 1,
>         "max_train_micro_batch_size_per_gpu": 1.024000e+03,
>         "min_train_micro_batch_size_per_gpu": 1,
>         "num_tuning_micro_batch_sizes": 3
>     }
>     [2023-01-11 13:27:59,213] [INFO] [config.py:1024:print]   bfloat16_enabled ............. False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   checkpoint_parallel_write_pipeline  False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   checkpoint_tag_validation_enabled  True
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   checkpoint_tag_validation_fail  False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   comms_config ................. <deepspeed.comm.config.DeepSpeedCommsConfig object at 0x7f32a7276b20>
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   communication_data_type ...... None
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   compression_config ........... {'weight_quantization': {'shared_parameters': {'enabled': False, 'quantizer_kernel': False, 'schedule_offset': 0, 'quantize_groups': 1, 'quantize_verbose': False, 'quantization_type': 'symmetric', 'quantize_weight_in_forward': False, 'rounding': 'nearest', 'fp16_mixed_quantize': False, 'quantize_change_ratio': 0.001}, 'different_groups': {}}, 'activation_quantization': {'shared_parameters': {'enabled': False, 'quantization_type': 'symmetric', 'range_calibration': 'dynamic', 'schedule_offset': 1000}, 'different_groups': {}}, 'sparse_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'row_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'head_pruning': {'shared_parameters': {'enabled': False, 'method': 'topk', 'schedule_offset': 1000}, 'different_groups': {}}, 'channel_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'layer_reduction': {'enabled': False}}
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   curriculum_enabled ........... False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   curriculum_params ............ False
>     Loading extension module fused_adam...
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   dataloader_drop_last ......... False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   disable_allgather ............ False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   dump_state ................... False
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   dynamic_loss_scale_args ...... None
>     Loading extension module fused_adam...
>     [2023-01-11 13:27:59,214] [INFO] [config.py:1024:print]   eigenvalue_enabled ........... False
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_gas_boundary_resolution  1
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_layer_name ........ bert.encoder.layer
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_layer_num ......... 0
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_max_iter .......... 100
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_stability ......... 1e-06
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_tol ............... 0.01
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   eigenvalue_verbose ........... False
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   elasticity_enabled ........... False
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   flops_profiler_config ........ {
>         "enabled": false,
>         "profile_step": 1,
>         "module_depth": -1,
>         "top_modules": 1,
>         "detailed": true,
>         "output_file": null
>     }
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   fp16_auto_cast ............... None
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   fp16_enabled ................. False
>     [2023-01-11 13:27:59,215] [INFO] [config.py:1024:print]   fp16_master_weights_and_gradients  False
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   global_rank .................. 0
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   grad_accum_dtype ............. None
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   gradient_accumulation_steps .. 1
>     Time to load fused_adam op: 50.09117794036865 seconds
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   gradient_clipping ............ 1.0
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   gradient_predivide_factor .... 1.0
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   initial_dynamic_scale ........ 4294967296
>     Time to load fused_adam op: 50.182053089141846 seconds
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   load_universal_checkpoint .... False
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   loss_scale ................... 0
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   memory_breakdown ............. False
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   monitor_config ............... <deepspeed.monitor.config.DeepSpeedMonitorConfig object at 0x7f32a7276a60>
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   nebula_config ................ {
>         "enabled": false,
>         "persistent_storage_path": null,
>         "persistent_time_interval": 100,
>         "num_of_version_in_retention": 2,
>         "enable_nebula_load": true,
>         "load_path": null
>     }
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   optimizer_legacy_fusion ...... False
>     [2023-01-11 13:27:59,216] [INFO] [config.py:1024:print]   optimizer_name ............... adam
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   optimizer_params ............. {'lr': 0.001, 'betas': [0.8, 0.999], 'eps': 1e-08, 'weight_decay': 3e-07}
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   pipeline ..................... {'stages': 'auto', 'partition': 'best', 'seed_layers': False, 'activation_checkpoint_interval': 0}
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   pld_enabled .................. False
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   pld_params ................... False
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   prescale_gradients ........... False
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   scheduler_name ............... WarmupLR
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   scheduler_params ............. {'warmup_min_lr': 0, 'warmup_max_lr': 0.001, 'warmup_num_steps': 1000}
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   sparse_attention ............. None
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   sparse_gradients_enabled ..... False
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   steps_per_print .............. 5
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   train_batch_size ............. 256
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   train_micro_batch_size_per_gpu  8
>     [2023-01-11 13:27:59,217] [INFO] [config.py:1024:print]   use_node_local_storage ....... False
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   wall_clock_breakdown ......... True
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   world_size ................... 32
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   zero_allow_untested_optimizer  False
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   zero_config .................. stage=0 contiguous_gradients=True reduce_scatter=True reduce_bucket_size=50000000 allgather_partitions=True allgather_bucket_size=50000000 overlap_comm=True load_from_fp32_weights=True elastic_checkpoint=False offload_param=None offload_optimizer=None sub_group_size=1,000,000,000 cpu_offload_param=None cpu_offload_use_pin_memory=None prefetch_bucket_size=50,000,000 param_persistence_threshold=100,000 model_persistence_threshold=sys.maxsize max_live_parameters=1,000,000,000 max_reuse_distance=1,000,000,000 gather_16bit_weights_on_model_save=False stage3_gather_fp16_weights_on_model_save=False ignore_unused_parameters=True legacy_stage1=False round_robin_gradients=False
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   zero_enabled ................. False
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1024:print]   zero_optimization_stage ...... 0
>     [2023-01-11 13:27:59,218] [INFO] [config.py:1009:print_user_config]   json = {
>         "train_batch_size": 256,
>         "steps_per_print": 5,
>         "optimizer": {
>             "type": "Adam",
>             "params": {
>                 "lr": 0.001,
>                 "betas": [0.8, 0.999],
>                 "eps": 1e-08,
>                 "weight_decay": 3e-07
>             }
>         },
>         "scheduler": {
>             "type": "WarmupLR",
>             "params": {
>                 "warmup_min_lr": 0,
>                 "warmup_max_lr": 0.001,
>                 "warmup_num_steps": 1000
>             }
>         },
>         "gradient_clipping": 1.0,
>         "prescale_gradients": false,
>         "fp16": {
>             "enabled": false,
>             "fp16_master_weights_and_grads": false,
>             "loss_scale": 0,
>             "loss_scale_window": 500,
>             "hysteresis": 2,
>             "min_loss_scale": 1,
>             "initial_scale_power": 15
>         },
>         "wall_clock_breakdown": true,
>         "zero_optimization": {
>             "stage": 0,
>             "allgather_partitions": true,
>             "reduce_scatter": true,
>             "allgather_bucket_size": 5.000000e+07,
>             "reduce_bucket_size": 5.000000e+07,
>             "overlap_comm": true,
>             "contiguous_gradients": true,
>             "cpu_offload": false
>         },
>         "comms_logger": {
>             "enabled": true,
>             "verbose": true,
>             "prof_all": true,
>             "debug": true
>         }
>     }
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.08269143104553 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.27721095085144 seconds
>     Time to load fused_adam op: 50.26706910133362 seconds
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.275376319885254 seconds
>     Time to load fused_adam op: 49.98901581764221 seconds
>     Time to load fused_adam op: 49.98150706291199 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.97796630859375 seconds
>     Time to load fused_adam op: 50.085554361343384 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Time to load fused_adam op: 49.980775356292725 seconds
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.97842764854431 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.97439670562744 seconds
>     Time to load fused_adam op: 49.974183082580566 seconds
>     Time to load fused_adam op: 49.975847482681274 seconds
>     Time to load fused_adam op: 49.97525334358215 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Time to load fused_adam op: 50.27005338668823 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.08176279067993 seconds
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.26860594749451 seconds
>     Time to load fused_adam op: 49.977802753448486 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.975820779800415 seconds
>     Time to load fused_adam op: 49.978567361831665 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Time to load fused_adam op: 50.263965368270874 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Time to load fused_adam op: 50.26710224151611 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.98522591590881 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.26634693145752 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 49.975499868392944 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Loading extension module fused_adam...
>     Loading extension module fused_adam...
>     Time to load fused_adam op: 50.18604803085327 seconds
>     Time to load fused_adam op: 50.18999457359314 seconds
>     Time to load fused_adam op: 50.19036340713501 seconds
>     Time to load fused_adam op: 50.17982244491577 seconds
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Using /home/foremans/.cache/torch_extensions/py38_cu114 as PyTorch extensions root...
>     Emitting ninja build file /home/foremans/.cache/torch_extensions/py38_cu114/utils/build.ninja...
>     Building extension module utils...
>     Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
>     [1/2] /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpicxx -MMD -MF flatten_unflatten.o.d -DTORCH_EXTENSION_NAME=utils -DTORCH_API_INCLUDE_EXTENSION_H -DPYBIND11_COMPILER_TYPE=\"_gcc\" -DPYBIND11_STDLIB=\"_libstdcpp\" -DPYBIND11_BUILD_ABI=\"_cxxabi1013\" -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/torch/csrc/api/include -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/TH -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/include/THC -isystem /lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/include/python3.8 -D_GLIBCXX_USE_CXX11_ABI=1 -fPIC -std=c++14 -c /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/argonne-lcf/mlprof/venvs/thetaGPU/2022-07-01/lib/python3.8/site-packages/deepspeed/ops/csrc/utils/flatten_unflatten.cpp -o flatten_unflatten.o
>     [2/2] /lus/theta-fs0/software/thetagpu/openmpi/openmpi-4.1.4_ucx-1.12.1_gcc-9.4.0/bin/mpicxx flatten_unflatten.o -shared -L/lus/theta-fs0/software/thetagpu/conda/2022-07-01/mconda3/lib/python3.8/site-packages/torch/lib -lc10 -ltorch_cpu -ltorch -ltorch_python -o utils.so
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.202441453933716 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.131984949111938 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.13672137260437 seconds
>     Time to load utils op: 14.136286735534668 seconds
>     Time to load utils op: 14.225647687911987 seconds
>     Time to load utils op: 14.136852979660034 seconds
>     Time to load utils op: 14.13709568977356 seconds
>     Time to load utils op: 14.225707054138184 seconds
>     Loading extension module utils...
>     Time to load utils op: 14.224344253540039 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.228283882141113 seconds
>     Time to load utils op: 14.22840166091919 seconds
>     Time to load utils op: 14.228489875793457 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.231348752975464 seconds
>     Time to load utils op: 14.22441840171814 seconds
>     Time to load utils op: 14.232226133346558 seconds
>     Time to load utils op: 14.224132776260376 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.224950790405273 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.22439169883728 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.223446607589722 seconds
>     Time to load utils op: 14.223729610443115 seconds
>     Time to load utils op: 14.220913410186768 seconds
>     Time to load utils op: 14.223800420761108 seconds
>     Time to load utils op: 14.223870038986206 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.221003532409668 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.220709323883057 seconds
>     Time to load utils op: 14.2245774269104 seconds
>     Time to load utils op: 14.22049617767334 seconds
>     Time to load utils op: 14.224029779434204 seconds
>     Time to load utils op: 14.222967863082886 seconds
>     Time to load utils op: 14.223030805587769 seconds
>     Loading extension module utils...
>     Loading extension module utils...
>     Time to load utils op: 14.226048707962036 seconds
>     Time to load utils op: 14.222215414047241 seconds
>     [2023-01-11 13:28:13,846][mlprof.trainers.pytorch.trainer][INFO] - [0] [1/10: 0/1875 (0%)] epoch=1.0000 step=1.0000 dt=0.3665 batch_acc=0.1094 batch_loss=0.0090 acc=0.0149 running_loss=0.0012
>     [2023-01-11 13:28:14,036][mlprof.trainers.pytorch.trainer][INFO] - [0] [1/10: 1280/1875 (62%)] epoch=1.0000 step=6.0000 dt=0.0025 batch_acc=0.5469 batch_loss=0.0063 acc=0.2709 running_loss=0.0066
>     [2023-01-11 13:28:15,366][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:15,366][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 71%
>     [2023-01-11 13:28:15,366][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:15,367][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:15,367][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0003  acc=1%
>     [2023-01-11 13:28:15,367][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:15,405][mlprof.trainers.pytorch.trainer][INFO] - [0] [2/10: 0/1875 (0%)] epoch=2.0000 step=9.0000 dt=0.0046 batch_acc=0.6758 batch_loss=0.0050 acc=0.0923 running_loss=0.0007
>     [2023-01-11 13:28:15,583][mlprof.trainers.pytorch.trainer][INFO] - [0] [2/10: 1280/1875 (62%)] epoch=2.0000 step=14.0000 dt=0.0022 batch_acc=0.6992 batch_loss=0.0035 acc=0.5723 running_loss=0.0033
>     [2023-01-11 13:28:16,897][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:16,898][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 85%
>     [2023-01-11 13:28:16,898][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:16,899][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:16,899][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0001  acc=2%
>     [2023-01-11 13:28:16,899][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:16,935][mlprof.trainers.pytorch.trainer][INFO] - [0] [3/10: 0/1875 (0%)] epoch=3.0000 step=17.0000 dt=0.0026 batch_acc=0.8086 batch_loss=0.0026 acc=0.1104 running_loss=0.0004
>     [2023-01-11 13:28:17,115][mlprof.trainers.pytorch.trainer][INFO] - [0] [3/10: 1280/1875 (62%)] epoch=3.0000 step=22.0000 dt=0.0023 batch_acc=0.7930 batch_loss=0.0024 acc=0.6667 running_loss=0.0019
>     [2023-01-11 13:28:18,415][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:18,415][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 90%
>     [2023-01-11 13:28:18,415][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:18,416][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:18,416][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0001  acc=3%
>     [2023-01-11 13:28:18,416][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:18,464][mlprof.trainers.pytorch.trainer][INFO] - [0] [4/10: 0/1875 (0%)] epoch=4.0000 step=25.0000 dt=0.0150 batch_acc=0.8633 batch_loss=0.0020 acc=0.1179 running_loss=0.0003
>     [2023-01-11 13:28:18,642][mlprof.trainers.pytorch.trainer][INFO] - [0] [4/10: 1280/1875 (62%)] epoch=4.0000 step=30.0000 dt=0.0149 batch_acc=0.8477 batch_loss=0.0019 acc=0.7019 running_loss=0.0016
>     [2023-01-11 13:28:19,939][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:19,939][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 92%
>     [2023-01-11 13:28:19,940][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:19,940][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:19,940][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0001  acc=3%
>     [2023-01-11 13:28:19,940][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:19,976][mlprof.trainers.pytorch.trainer][INFO] - [0] [5/10: 0/1875 (0%)] epoch=5.0000 step=33.0000 dt=0.0026 batch_acc=0.8867 batch_loss=0.0015 acc=0.1211 running_loss=0.0002
>     [2023-01-11 13:28:20,154][mlprof.trainers.pytorch.trainer][INFO] - [0] [5/10: 1280/1875 (62%)] epoch=5.0000 step=38.0000 dt=0.0022 batch_acc=0.8984 batch_loss=0.0016 acc=0.7152 running_loss=0.0013
>     [2023-01-11 13:28:20,248][mlprof.trainers.pytorch.trainer][INFO] - [0] [6/10: 0/1875 (0%)] epoch=6.0000 step=41.0000 dt=0.0026 batch_acc=0.9062 batch_loss=0.0014 acc=0.1237 running_loss=0.0002
>     [2023-01-11 13:28:20,425][mlprof.trainers.pytorch.trainer][INFO] - [0] [6/10: 1280/1875 (62%)] epoch=6.0000 step=46.0000 dt=0.0024 batch_acc=0.9102 batch_loss=0.0012 acc=0.7397 running_loss=0.0011
>     [2023-01-11 13:28:21,724][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:21,725][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 94%
>     [2023-01-11 13:28:21,725][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:21,725][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:21,726][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0000  acc=3%
>     [2023-01-11 13:28:21,726][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:21,762][mlprof.trainers.pytorch.trainer][INFO] - [0] [7/10: 0/1875 (0%)] epoch=7.0000 step=49.0000 dt=0.0026 batch_acc=0.8984 batch_loss=0.0012 acc=0.1227 running_loss=0.0002
>     [2023-01-11 13:28:21,941][mlprof.trainers.pytorch.trainer][INFO] - [0] [7/10: 1280/1875 (62%)] epoch=7.0000 step=54.0000 dt=0.0023 batch_acc=0.8828 batch_loss=0.0014 acc=0.7344 running_loss=0.0011
>     [2023-01-11 13:28:23,250][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:23,250][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 95%
>     [2023-01-11 13:28:23,251][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:23,251][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:23,251][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0000  acc=3%
>     [2023-01-11 13:28:23,251][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:23,288][mlprof.trainers.pytorch.trainer][INFO] - [0] [8/10: 0/1875 (0%)] epoch=8.0000 step=57.0000 dt=0.0026 batch_acc=0.9180 batch_loss=0.0011 acc=0.1253 running_loss=0.0002
>     [2023-01-11 13:28:23,468][mlprof.trainers.pytorch.trainer][INFO] - [0] [8/10: 1280/1875 (62%)] epoch=8.0000 step=62.0000 dt=0.0023 batch_acc=0.9297 batch_loss=0.0010 acc=0.7461 running_loss=0.0009
>     [2023-01-11 13:28:24,785][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:24,785][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 95%
>     [2023-01-11 13:28:24,786][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:24,786][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:24,786][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0000  acc=3%
>     [2023-01-11 13:28:24,786][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:24,835][mlprof.trainers.pytorch.trainer][INFO] - [0] [9/10: 0/1875 (0%)] epoch=9.0000 step=65.0000 dt=0.0148 batch_acc=0.9102 batch_loss=0.0011 acc=0.1243 running_loss=0.0001
>     [2023-01-11 13:28:25,015][mlprof.trainers.pytorch.trainer][INFO] - [0] [9/10: 1280/1875 (62%)] epoch=9.0000 step=70.0000 dt=0.0148 batch_acc=0.9258 batch_loss=0.0011 acc=0.7515 running_loss=0.0009
>     [2023-01-11 13:28:26,313][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:26,313][mlprof.trainers.pytorch.trainer][INFO] - [TEST] Accuracy: 96%
>     [2023-01-11 13:28:26,314][mlprof.trainers.pytorch.trainer][INFO] - --------------------
>     [2023-01-11 13:28:26,314][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:26,314][mlprof.trainers.pytorch.trainer][INFO] - [TRAIN]  loss=0.0000  acc=3%
>     [2023-01-11 13:28:26,314][mlprof.trainers.pytorch.trainer][INFO] - ----------------------------
>     [2023-01-11 13:28:26,351][mlprof.trainers.pytorch.trainer][INFO] - [0] [10/10: 0/1875 (0%)] epoch=10.0000 step=73.0000 dt=0.0026 batch_acc=0.9297 batch_loss=0.0008 acc=0.1269 running_loss=0.0001
>     [2023-01-11 13:28:26,530][mlprof.trainers.pytorch.trainer][INFO] - [0] [10/10: 1280/1875 (62%)] epoch=10.0000 step=78.0000 dt=0.0023 batch_acc=0.9258 batch_loss=0.0010 acc=0.7589 running_loss=0.0009
>     [2023-01-11 13:28:26,589][mlprof.trainers.pytorch.trainer][INFO] - [0] :: Total training time: 13.143308877944946 seconds
>     [2023-01-11 13:28:26,589][mlprof.trainers.pytorch.trainer][INFO] - [0] :: Average time per epoch in the last 5: 0.2688056468963623
>     ```