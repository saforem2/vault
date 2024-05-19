---
tags:
    - "#megatron-deepspeed"
    - "#LLMs"
    - "#Aurora"
---

# Intel LLMs

![weak-scaling](./assets/image001.png)

## 2023-12-21

- [ ] Send example test using `ezpz`

### `ezpz`

```bash
$ python3 -m pip install ezpz
<output-here>
```

- [x] Working on Aurora

    ```bash
    # launch job
    $ qsub -q EarlyAppAccess -A Aurora_Deployment -l walltime=2:00:00 -l select=4 -I
    # load frameworks
    $ module use -a /soft/modulefiles ; module --ignore_cache load frameworks
    $ module load frameworks/.2023.12.15.001
    # install `ezpz`
    $ git clone https://github.com/saforem2/ezpz
    $ cd ezpz
    $ mkdir -p venvs/aurora/2023.12.15.001
    $ python3 -m venv venvs/aurora/2023.12.15.001 --system-site-packages
    $ source venvs/aurora/2023.12.15.001/bin/activate
    $ python3 -m pip install -e .
    # print job info and define `launch` alias
    $ source ezpz/src/ezpz/bin/savejobenv
    ┌──────────────────────────────────────────────────────────────────
    │ [Hosts]:
    │     • x4415c6s5b0n0.hostmgmt2415.cm.aurora.alcf.anl.gov
    x4415c6s6b0n0.hostmgmt2415.cm.aurora.alcf.anl.gov
    x4415c6s7b0n0.hostmgmt2415.cm.aurora.alcf.anl.gov
    x4415c7s0b0n0.hostmgmt2415.cm.aurora.alcf.anl.gov
    └──────────────────────────────────────────────────────────────────
    ┌──────────────────────────────────────────────────────────────────
    │ [DIST INFO]:
    │     • Loading job env from: /home/foremans/.pbsenv
    │     • HOSTFILE: /var/spool/pbs/aux/297306.aurora-pbs-0001.hostmgmt.cm.aurora.alcf.anl.gov
    │     • NHOSTS: 4
    │     • NGPU_PER_HOST: 12
    │     • NGPUS (NHOSTS x NGPU_PER_HOST): 48
    │     • DIST_LAUNCH: mpiexec --verbose --envall -n 48 -ppn 12 --hostfile /var/spool/pbs/aux/297306.aurora-pbs-0001.hostmgmt.cm.aurora.alcf.anl.gov
    │     • Defining alias: launch: aliased to mpiexec --verbose --envall -n 48 -ppn 12 --hostfile /var/spool/pbs/aux/297306.aurora-pbs-0001.hostmgmt.cm.aurora.alcf.anl.gov
    └──────────────────────────────────────────────────────────────────

    # ----------------------------------------------------------
    # launch + startup on all workers with
    # • `framework` ∈ {`pytorch`, `tensorflow`}
    # • `backend` ∈ {`horovod`, `deepspeed`, `DDP`}
    # where `deepspeed` and `DDP` only available for `pytorch`
    # ----------------------------------------------------------

    $ launch python3 -m ezpz framework=pytorch backend=DDP
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:24][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:25][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:26][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:26][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:26][INFO][dist.py:243] - Using DDP for distributed training
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:26][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:27][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:28][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:28][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:29][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:29][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:29][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:30][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:34][INFO][dist.py:292] - Using device='xpu'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][WARNING][dist.py:104] - Using backend='ccl'
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 1 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 2 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 3 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 4 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 0 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 5 / 47
    [2023-12-19 13:33:35][INFO][__main__.py:49] - {
        "_target_": "ezpz.configs.TrainConfig",
        "framework": "pytorch",
        "backend": "DDP",
        "ds_config_path": null,
        "port": null,
        "seed": null,
        "use_wandb": true,
        "wandb_project_name": null,
        "precision": null,
        "ngpus": null
    }
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 9 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 10 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 11 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 7 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 8 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 6 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 12 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 13 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 14 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 15 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 18 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 19 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 20 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 21 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 22 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 23 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 24 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 25 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 26 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 27 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 30 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 16 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 17 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 28 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 32 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 33 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 36 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 37 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 38 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 39 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 43 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 46 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 29 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 47 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 31 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 34 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 35 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 42 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 41 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 44 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 45 / 47
    [2023-12-19 13:33:35][INFO][dist.py:307] - RANK: 40 / 47
    [2023-12-19 13:33:47][INFO][dist.py:415] - Setting up wandb from rank: 0
    [2023-12-19 13:33:47][INFO][dist.py:416] - Using: WB PROJECT: ezpz
    [2023-12-19 13:33:58][INFO][dist.py:448] - W&B RUN: [flowing-wood-8](https://wandb.ai/l2hmc-qcd/ezpz/runs/uya29gm5)
    [2023-12-19 13:33:58][INFO][dist.py:490] - Running on x4415c6s5b0n0.hostmgmt2415.cm.aurora.alcf.anl.gov
    [2023-12-19 13:33:58][INFO][dist.py:506] - Reading hosts from /var/spool/pbs/aux/297306.aurora-pbs-0001.hostmgmt.cm.aurora.alcf.anl.gov
    [2023-12-19 13:33:58][INFO][__main__.py:57] - Output dir: /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/outputs/runs/pytorch/DDP/2023-12-19/13-33-17
    [2023-12-19 13:33:58][CRITICAL][dist.py:519] - 🚀 flowing-wood-8
    [2023-12-19 13:33:58][CRITICAL][dist.py:520] - 🔗 https://wandb.ai/l2hmc-qcd/ezpz/runs/uya29gm5
    [2023-12-19 13:33:58][CRITICAL][dist.py:521] - 📂/: /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/outputs/runs/pytorch/DDP/2023-12-19/13-33-17/wandb/run-20231219_133354-uya29gm5/files
    [2023-12-19 13:33:58][INFO][dist.py:563] - Adding /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/ezpz-pt-DDP-xpu.log to W&B artifact...
    [2023-12-19 13:33:58][INFO][dist.py:563] - Adding /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/outputs/runs/pytorch/DDP/2023-12-19/13-33-17/__main__.log to W&B artifact...
    [2023-12-19 13:33:58][INFO][dist.py:563] - Adding /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/outputs/runs/pytorch/DDP/2023-12-19/13-33-17/main_debug.log to W&B artifact...
    [2023-12-19 13:33:58][INFO][dist.py:563] - Adding /lus/gecko/projects/Aurora_deployment/foremans/projects/saforem2/ezpz/src/ezpz/outputs/runs/pytorch/DDP/2023-12-19/13-33-16/__main__.log to W&B artifact...
    ```

- From Tanima:

  > Hi Sam and Corey,
  > Thanks for your comments on measuring the application start up time last
  > week. Typically, we report the throughput performance after the start-up
  > and warm-up during the “steady” state of the training. We have a few
  > follow-up questions so that we establish a methodology to address the issue
  > brought up by Argonne. We can set a few timestamps in the model scripts and
  > job scripts used for the queue submission:
  >
  > Job script:
  >     ```bash
  >     Time stamp A:
  >     \<actual python command using mpiexec>
  >
  >     Inside the model script:
  >     main()
  >     Timestamp B:
  >
  >     Timestamp C:
  >                First training steps and onwards.
  >     By startup time, do you mean measuring time difference between A and C
  >     or B and C?
  >
  >     Will the measurement methodology be the same for distributed training?
  >     For examples, we can measure the start-up time for the rank0?
  >
  >     If we need to report the startup time for the DL applications, do we
  >     need to collect measurements using the actual Aurora NRE workloads or
  >     some small benchmarking test cases? For example, we can try to recreate
  >     the typical start-up scenarios, like library imports, and measure those
  >     separately as shown below.
  >     ```
  >
  > Job script:
  >
  >     ```bash
  >     Time stamp A:
  >     <actual python command using mpiexec>
  >
  >     Time stamp B:
  >     import torch
  >     Time stamp C
  >     import IPEX
  >     Time stamp D
  >     Etc...
  >     ```
  >
  > If you have any other scenarios, please feel free to suggest.
  >
  > Thanks,
  > Tanima.

## 2023-12-04

- [x] Get initialization times from Megatron DeepSpeed runs

    ```bash
    $ for f in $(tail -5 logfiles) ;
    for> do echo $f; \
    for> cat $f | grep -E "Job started|step=0\," | uniq ; \
    for> echo "\n" ; done > init_times.txt
    /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/Megatron-DeepSpeed/outputs/gpt_actCkpt_GPT1T_4L_z1_seqlen2048_mp8_pp2_sp1_nl4_hs25600_gb16_mb1/logs/foremans-x3004c0s13b0n0-nhosts4-ngpu16-2023-11-02-183323.log
    Job started at: 2023-11-02-183323 on x3004c0s13b0n0
    [2023-11-02 18:34:13,122] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]

    /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/Megatron-DeepSpeed/outputs/gpt_SP_actCkpt_GPT125M_z0_seqlen2048_mp16_pp1_sp1_nl12_hs768_gb1_mb1/logs/foremans-x3015c0s37b0n0-nhosts4-ngpu16-2023-11-02-184240.log
    Job started at: 2023-11-02-184240 on x3015c0s37b0n0

    /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/Megatron-DeepSpeed/outputs/gpt_SP_actCkpt_GPT125M_z0_seqlen2048_mp16_pp1_sp1_nl12_hs768_gb1_mb1/logs/foremans-x3015c0s37b0n0-nhosts4-ngpu16-2023-11-02-184259.log
    Job started at: 2023-11-02-184259 on x3015c0s37b0n0
    [2023-11-02 18:43:23,385] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]

    /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/Megatron-DeepSpeed/outputs/gpt_SP_actCkpt_GPT125M_z0_seqlen2048_mp16_pp1_sp1_nl12_hs768_gb1_mb1/logs/foremans-x3004c0s13b0n0-nhosts4-ngpu16-2023-11-02-184407.log
    Job started at: 2023-11-02-184407 on x3004c0s13b0n0
    [2023-11-02 18:44:32,804] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]

    /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/Megatron-DeepSpeed/outputs/gpt_actCkpt_GPT1T_4L_z1_seqlen2048_mp8_pp2_sp1_nl4_hs25600_gb16_mb2/logs/foremans-x3108c0s25b1n0-nhosts2-ngpu8-2023-11-02-192739.log
    Job started at: 2023-11-02-192739 on x3108c0s25b1n0
    [2023-11-02 19:29:18,388] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]
    ```


- 1st line: e.g. `Job started at: 2023-11-02-184407 on x3004c0s13b0n0`

    - Cut `Job started at: ` from timestamps:
    	```bash
         $ /bin/cat init_times.txt | sed "s/Job\ started\ at\:\ //g" > init_times1.txt
    	```
     
- 2nd line: e.g. `[2023-11-02 18:44:32,804] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]`

    - Cut `] [INFO] [...]`:
    
        ```bash
        /bin/cat init_times1.txt| sed "s/^\[//g" | sed "s/\].*//g" | sed "s/\ on\ .*$//g" | sed "s/\ /-/g" | sed "s/\://g"
        ```

> [!summary]+ Combined
> 1. Get times from `logfiles`:
>
>     ```bash
>     $ for f in $(tail -5 logfiles) ; do echo $f; cat $f | grep -E "Job started|step=0\," | uniq ; echo "\n" ; done > init_times.txt
>     ```
> 
> 2. Clean timestamps for comparison:
> 
> 	```bash
> 	/bin/cat init_times.txt | sed "s/Job\ started\ at\:\ //g" | sed "s/^\[//g" | sed "s/\].*//g" | sed "s/\ \on\ .*$//g" | sed "s/\ /-/g" | sed "s/\://g" | sed "s/\,.*//g"
> 	```

- Process with Python:

```python
>>> import numpy as np
>>> from pathlib import Path
>>> fpath = Path('./init_times1.txt')
>>> with fpath.open('r') as f:
...     tmp = [i.rstrip('\n') for i in f.readlines()]
>>> logfiles = tmp[::3]
>>> assert all([i.startswith('/') for i in logfiles])
>>> t0 = tmp[1::3]
>>> t1 = tmp[2::3]
>>> t0_arr = np.array([int(i.split('-')[-1]) for i in t0])
>>> t1_arr = np.array([int(i.split('-')[-1]) for i in t1])
>>> dt_arr = t1_arr - t0_arr
>>> data = {}
... for idx, logfile in enumerate(logfiles):
...     stem = '/'.join(logfile.split('/')[-3:]).replace('logs/', '')
...     #data['gpt_SP_actCkpt_GPT1_5B_z0_seqlen2048_mp8_pp1_sp1_nl48_hs1536_gb1_mb1/foremans-x3005c0s25b1n0-nhosts2-ngpu8-2023-10-10-182743.log']
...     #model_size = stem.split('/')[0].split('_')[2:5][-2:]
...     model_size = stem.split('/')[0].split('_z')[0].split('_')[-2:]
...     world_size = int(stem.split('/')[1].split('-')[3].lstrip('ngpu'))
...     data[stem] = {
...         'model_size': model_size,
...         'world_size': world_size,
...         'start': t0[idx],
...         'end': t1[idx],
...         't0': t0_arr[idx],
...         't1': t1_arr[idx],
...         'dt': dt_arr[idx],
...     }
>>> df = pd.DataFrame.from_dict(data)
>>> df.T.to_csv('./init_times_calc3.csv')
```

### Perlmutter

```bash
$ for f in $(/bin/cat logfiles) ; do echo $f; cat $f | grep -E "Job started|step=0\," | uniq ; echo "\n" ; done > init_times.txt
$ /bin/cat init_times.txt | sed "s/Job\ started\ at\:\ //g" | sed "s/^.*0\[//g" | sed "s/\].*//g" | sed "s/\ \on\ .*$//g" | sed "s/\ /-/g" | sed "s/\://g" | sed "s/\,.*//g" | sed "s/^.*\[//g" > init_times1.txt

### 25B Architecture

From Gautham:
```json
"architectures": [
    "GPTNeoXForCausalLM"
  ],
  "attention_probs_dropout_prob": 0.1,
  "bos_token_id": 0,
  "eos_token_id": 0,
  "hidden_act": "gelu_fast",
  "hidden_dropout_prob": 0.1,
  "hidden_size": 8196,
  "initializer_range": 0.02,
  "intermediate_size": 8000,
  "layer_norm_eps": 1e-05,
  "max_position_embeddings": 2048,
  "model_type": "gpt_neox",
  "num_attention_heads": 64,
  "num_hidden_layers": 64,
  "rotary_emb_base": 10000,
  "rotary_pct": 0.25,
  "tie_word_embeddings": false,
  "torch_dtype": "float32",
  "transformers_version": "4.27.2",
  "use_cache": true,
  "use_deepspeed_checkpointing": true,
  "use_parallel_residual": true,
  "vocab_size": 69
  ```

## 2023-11

### PP Scaling

![Pipeline-Parallelism-Scaling-Perlmutter](Pipeline-Parallelism-Scaling-Perlmutter.md)

### 2023-10-18

#### Data Parallelism Scaling

##### MBS=1

| DP  | TFLOPS | scaling (\%)|
| --- |:------:|:-------:|
| 1   |  52.8  |  100   |
| 2   |  37.4  |   71   |
| 4   |  32.9  |   62   |
| 8   |  30.9  |   59   |
^dp-mbs1

: [Table: Data Parallelism Scaling, `MBS=1` ](#tbl-dp-mbs1) Detailed Data Parallelism Scaling Results on Intel GPU with `MICRO_BATCH_SIZE=1` {#tbl-dp-mbs1}

##### MBS=2  

| TFLOPS | scaling |
|:------:|:-------:|
| 63.8   | 100%    |
| 51.2   | 80%     |
| 46.7   | 73%     |
| 44.4   | 70%     |
^dp-mbs2

: [Table: Data Parallelism Scaling, `MBS=2` ](#tbl-dp-mbs2) Detailed Data Parallelism Scaling Results on Intel GPU with `MICRO_BATCH_SIZE=2` {#tbl-dp-mbs2}

##### MBS=

| TFLOPS | scaling |
|:------:|:-------:|
| 71.1   | 100%    |
| 63.7   | 90%     |
| 59.2   | 83%     |
| 57.5   | 81%     |
^dp-mb4

: [Table: Data Parallelism Scaling, `MBS=4` ](#tbl-dp-mbs4) Detailed Data Parallelism Scaling Results on Intel GPU with `MICRO_BATCH_SIZE=4` {#tbl-dp-mbs4}

### 2023-10-10

```json
{
	"MODEL_SIZE": "GPT1T_2L",
	"machine": "Perlmutter",
	"world_size": 64,
	"env.SP_TYPE": "megatron",
	"args.micro_batch_size": 4,
	"args.seq_length": 2048,
	"args.global_batch_size": 256,
	"args.zero_stage": 1,
	"args.tensor_model_parallel_size": 8,
	"args.pipeline_model_parallel_size": 1,
	"args.data_parallel_size": 8
}
```

```bash
-------------------------- DeepSpeed Flops Profiler --------------------------
Profile Summary at step 2:
Notations:
data parallel size (dp_size), model parallel size(mp_size),
number of parameters (params), number of multiply-accumulate operations(MACs),
number of floating-point operations (flops), floating-point operations per second (FLOPS),
fwd latency (forward propagation latency), bwd latency (backward propagation latency),
step (weights update latency), iter latency (sum of fwd, bwd and step latency)
world size:                                                             64
data parallel size:                                                     8
model parallel size:                                                    8
batch size per GPU:                                                     4
params per GPU:                                                         2.14 B
params of model = params per GPU * mp_size:                             17.1 B
fwd MACs per GPU:                                                       17.66 TMACs
fwd flops per GPU:                                                      35.33 T
fwd flops of model = fwd flops per GPU * mp_size:                       282.61 T
fwd latency:                                                            1.55 s
fwd FLOPS per GPU = fwd flops per GPU / fwd latency:                    22.85 TFLOPS
bwd latency:                                                            4.92 s
bwd FLOPS per GPU = 2 * fwd flops per GPU / bwd latency:                14.37 TFLOPS
fwd+bwd FLOPS per GPU = 3 * fwd flops per GPU / (fwd+bwd latency):      16.4 TFLOPS
step latency:                                                           1.31 s
iter latency:                                                           7.77 s
FLOPS per GPU = 3 * fwd flops per GPU / iter latency:                   13.63 TFLOPS
samples/second:                                                         32.93
----------------------------- Aggregated Profile per GPU -----------------------------
```

### 2023-10-03

#### TODO
- Try turning off activation checkpointing to figure out PP > 1 errors
- Work with Huihuo / Murali to figure out why TFLOPS increasing with DPSIZE on
    ![](assets/ScreenShot-2023-10-04-142126.png)

> [!TODO]+ From Deepak:
> > Venkat/Sam,
> > We are seeing an improvement in DP scaling efficiency as the number of PP stages increases.
> > Could you try reproducing this on Polaris/Perlmutter, even with a smaller model that fits in 1 node ?
> 
> |   |   |   |   |
> |---|---|---|---|
> |`TP=12, MBS=2, GAS=8*PP, NLAYERS=2*PP`|   |   |   |
> |||||
> ||`DP=1`|`DP=2`|`scaling`|
> |||||
> |`PP=1`|63.8|51.2|80.3%|
> |`PP=2`|64.8|57.1|88.1%|
> |`PP=8`|66.8|63.4|94.9%|
> |`PP=16`|67.5|65.6|97.2%|
>

## Intel Results

- Pipeline Scaling `{GAS: 8 * PP, NLAYERS: 2 * PP}`

|**PP**|**LAYERS**|**MBS**|**GBS**|**TFLOPS**|**sample/s**|
|---|---|---|---|---|---|
|2|4|1|16|54.7|2.5|
||4|2|32|64.8|2.9|
||4|4|64|71.6|3.2|
|||||||
|8|16|1|64|59.4|2.7|
||16|2|128|66.8|3.1|
|||||||
|16|32|1|128|60.5|2.8|
||32|2|256|67.5|3.1|
|||||||
|32|64|1|256|60.0|2.8|
||64|2|512|OOM|OOM|
||62|2|512|67.5|3.2|

- Data-parallel scaling `{PP=1}`

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|**TP=12, PP=1, GAS=8**|   ||||||
||||||||
||**MBS=1**|   |**MBS=2**|   |**MBS=4**|   |
|**DP**|**TFLOPS**|**scaling**|**TFLOPS**|**scaling**|**TFLOPS**|**scaling**|
||||||||
|1|52.8|100%|63.8|100%|71.1|100%|
|2|37.4|71%|51.2|80%|63.7|90%|
|4|32.9|62%|46.7|73%|59.2|83%|
|8|30.9|59%|44.4|70%|57.5|81%|
