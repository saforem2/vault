# Megatron DeepSpeed (rebase)




> [!BUG]- Training Bug
> ```Shell
>  /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-  │
> │ Benchmarking/megatron/training.py:733 in train_step                                              │
> │                                                                                                  │
> │    730 │   │   increment = get_num_microbatches() * \                                            │
> │    731 │   │   │   │   │   args.micro_batch_size * \                                             │
> │    732 │   │   │   │   │   args.data_parallel_size                                               │
> │ ❱  733 │   │   model[0].step(lr_kwargs={'increment': increment})                                 │
> │    734 │   │   update_successful = model[0].was_step_applied()                                   │
> │    735 │   else:                                                                                 │
> │    736 │   │   update_successful, grad_norm, num_zeros_in_grad = optimizer.step()                │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py:2 │
> │ 084 in step                                                                                      │
> │                                                                                                  │
> │   2081 │   │   │   │   │   and self.quantizer.any_precision_switch()):                           │
> │   2082 │   │   │   │   self._take_model_step(lr_kwargs, self.block_eigenvalue)                   │
> │   2083 │   │   │   else:                                                                         │
> │ ❱ 2084 │   │   │   │   self._take_model_step(lr_kwargs)                                          │
> │   2085 │   │   │                                                                                 │
> │   2086 │   │   │   report_progress = self.global_rank == 0 if self.global_rank else True         │
> │   2087                                                                                           │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py:2 │
> │ 038 in _take_model_step                                                                          │
> │                                                                                                  │
> │   2035 │   │   │   │   │   # XXX Hack to work with Megatron 2.0 and DeepSpeed pipelines.         │
> │   2036 │   │   │   │   │   # We don't currently have a way to specify lr_kwargs from             │
> │   2037 │   │   │   │   │   # pipe_engine.train_batch()                                           │
> │ ❱ 2038 │   │   │   │   │   self.lr_scheduler.step(increment=self.train_batch_size())             │
> │   2039 │   │                                                                                     │
> │   2040 │   │   if report_progress and (self.global_steps + 1) % self.steps_per_print() == 0:     │
> │   2041 │   │   │   self._report_progress(self.global_steps + 1)                                  │
> ╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
> TypeError: WarmupLR.step() got an unexpected keyword argument 'increment'
> ```
> 

# LR Increment ???
- Crashes with:

> [!BUG]+ Training Bug
> ```bash
> MICRO_BATCH=4 WORLD_SIZE=8 SP_TYPE="megatron" SPSIZE=1 PPSIZE=1 MPSIZE=1 ZERO_STAGE=1 USE_SEQUENCE_PARALLEL=1 ./ALCF/train-gpt3.sh
> /usr/share/lmod/lmod/init/sh: line 15: export: __add_sys_prefix_to_path: not a function
> source-ing /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF/launch.sh
> source-ing /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF/args.sh
> ------------------------
> SCRIPT_DIR=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF
> SCRIPT_PATH=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF/args.sh
> ------------------------
> SOURCE=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF/args.sh
> DIR=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF
> ------------------------
> +++++++++++++++++++++++++++
> Using GPT125M
> +++++++++++++++++++++++++++
> source-ing /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF/model.sh
> NHOSTS * (NGPU / HOST) = 2 * 4 = 8
> GB = NGPUS * MB * GAS = 8 * 4 * 1 = 32
> GB = (NGPUS * MB * GAS) / (MP * PP * SP) = (8 * 4 * 1) / (1 * 1 * 1) = 32
> --------------------------------
> GLOBAL_BATCH=32
> --------------------------------
> OUTPUT TO: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4
> ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
> gpt_args:     --sequence-parallel         --checkpoint-activations     --checkpoint-num-layers 1       --seed 19855   --DDP-impl local   --cpu-optimizer   --pipeline-model-parallel-size 1   --tensor-model-parallel-size 1   --sequence-parallel-size 1   --num-layers 12   --hidden-size 768   --num-attention-heads 16   --micro-batch-size 4   --global-batch-size 32   --seq-length 1024   --max-position-embeddings 1024   --train-iters 5   --lr-decay-iters 320000   --num-workers 1   --data-path /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document --vocab-file /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-vocab.json --merge-file /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-merges.txt   --data-impl mmap   --split 949,50,1   --distributed-backend nccl   --lr 0.00015   --lr-decay-style cosine   --min-lr 1.0e-5   --weight-decay 1e-2   --clip-grad 1.0   --lr-warmup-fraction .01   --log-interval 1   --save-interval 1000 --eval-interval 1000   --eval-iters 1   --override-opt_param-scheduler   --tensorboard-dir /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/tensorboard   --log-timers-to-tensorboard   --tensorboard-log-interval 1    --fp16  --cpu-optimizer  --deepspeed-activation-checkpointing --no-pipeline-parallel  --zero-stage=1  --deepspeed_config=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ds_config-gpt.json  --deepspeed_mpi  --deepspeed
> ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
> ./ALCF/train-gpt3.sh: line 38: setup: command not found
>     Running on 2 hosts     with 4 GPUs each     for a total of 8 GPUs
> Job started at: 2023-08-08-162815 on x3211c0s1b1n0
> Job running in: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF
> Training GPT-3 with GPT125M parameters
> Writing logs to: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4
> to view output: tail -f $(tail -1 logfiles)
> i.e. tail -f /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/logs/foremans-x3211c0s1b1n0-nhosts2-ngpu8-2023-08-08-162815.log
> using: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/bin/python3
> Job started at: 2023-08-08-162815 on x3211c0s1b1n0
> Job running in: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ALCF
> Training GPT-3 with GPT125M parameters
> Writing logs to: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4
> to view output: tail -f $(tail -1 logfiles)
> i.e. tail -f /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/logs/foremans-x3211c0s1b1n0-nhosts2-ngpu8-2023-08-08-162815.log
> EXEC=   /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/bin/python3 /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/pretrain_gpt.py     --sequence-parallel         --checkpoint-activations     --checkpoint-num-layers 1       --seed 19855   --DDP-impl local   --cpu-optimizer   --pipeline-model-parallel-size 1   --tensor-model-parallel-size 1   --sequence-parallel-size 1   --num-layers 12   --hidden-size 768   --num-attention-heads 16   --micro-batch-size 4   --global-batch-size 32   --seq-length 1024   --max-position-embeddings 1024   --train-iters 5   --lr-decay-iters 320000   --num-workers 1   --data-path /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document --vocab-file /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-vocab.json --merge-file /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-merges.txt   --data-impl mmap   --split 949,50,1   --distributed-backend nccl   --lr 0.00015   --lr-decay-style cosine   --min-lr 1.0e-5   --weight-decay 1e-2   --clip-grad 1.0   --lr-warmup-fraction .01  --log-interval 1   --save-interval 1000   --eval-interval 1000   --eval-iters 1   --override-opt_param-scheduler   --tensorboard-dir /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/tensorboard   --log-timers-to-tensorboard   --tensorboard-log-interval 1    --fp16  --cpu-optimizer  --deepspeed-activation-checkpointing --no-pipeline-parallel  --zero-stage=1  --deepspeed_config=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ds_config-gpt.json  --deepspeed_mpi  --deepspeed--deepspeed-activation-checkpointing --no-pipeline-parallel  --zero-stage=1  --deepspeed_config=/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ds_config-gpt.json  --deepspeed_mpi  --deepspeed
> Writing logs to: /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/logs/foremans-x3211c0s1b1n0-nhosts2-ngpu8-2023-08-08-162815.log
> [2023-08-08 16:28:20,489] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to cuda (auto detect)
> 2023-08-08 16:28:22.783869: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  SSE3 SSE4.1 SSE4.2 AVX AVX2 FMA
> To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
> [2023-08-08 16:28:26,245] [INFO] [comm.py:631:init_distributed] cdb=None
> [2023-08-08 16:28:26,245] [INFO] [comm.py:646:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
> [2023-08-08 16:28:26,251] [INFO] [comm.py:696:mpi_discovery] Discovered MPI settings of world_rank=0, local_rank=0, world_size=1, master_addr=10.140.58.153, master_port=29500
> [2023-08-08 16:28:26,251] [INFO] [comm.py:662:init_distributed] Initializing TorchBackend in DeepSpeed with backend nccl
> wandb: Currently logged in as: saforem2 (l2hmc-qcd). Use `wandb login --relogin` to force relogin
> wandb: wandb version 0.15.8 is available!  To upgrade, please run:
> wandb:  $ pip install wandb --upgrade
> wandb: Tracking run with wandb version 0.13.10
> wandb: Run data is saved locally in /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/tensorboard/wandb/run-20230808_162828-14ynrmls
> wandb: Run `wandb offline` to turn off syncing.
> wandb: Syncing run 1kseq-len-new-32global-batch-1GPUs-1MP-1PP-16-28
> wandb: ⭐️ View project at https://wandb.ai/l2hmc-qcd/Megatron-DS1
> wandb: 🚀 View run at https://wandb.ai/l2hmc-qcd/Megatron-DS1/runs/14ynrmls
> --------------------------------------------------
> DeepSpeed C++/CUDA extension op report
> --------------------------------------------------
> NOTE: Ops not installed will be just-in-time (JIT) compiled at
>       runtime if needed. Op compatibility means that your system
>       meet the required dependencies to JIT install the op.
> --------------------------------------------------
> JIT compiled ops requires ninja
> ninja .................. [OKAY]
> --------------------------------------------------
> op name ................ installed .. compatible
> --------------------------------------------------
>  [WARNING]  async_io requires the dev libaio .so object and headers but these were not found.
>  [WARNING]  async_io: please install the libaio-devel package with yum
>  [WARNING]  If libaio is already installed (perhaps from source), try setting the CFLAGS and LDFLAGS environment variables to where it can be found.
> async_io ............... [YES] ...... [NO]
> fused_adam ............. [YES] ...... [OKAY]
> cpu_adam ............... [YES] ...... [OKAY]
> cpu_adagrad ............ [YES] ...... [OKAY]
> fused_lamb ............. [YES] ...... [OKAY]
> quantizer .............. [YES] ...... [OKAY]
> random_ltd ............. [YES] ...... [OKAY]
>  [WARNING]  using untested triton version (2.0.0), only 1.0.0 is known to be compatible
> sparse_attn ............ [NO] ....... [NO]
> spatial_inference ...... [YES] ...... [OKAY]
> transformer ............ [YES] ...... [OKAY]
> stochastic_transformer . [YES] ...... [OKAY]
> transformer_inference .. [YES] ...... [OKAY]
> --------------------------------------------------
> DeepSpeed general environment info:
> torch install path ............... ['/soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch']
> torch version .................... 1.13.0a0+git49444c3
> deepspeed install path ........... ['/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed']
> deepspeed info ................... 0.10.1+57a27b08, 57a27b08, master
> torch cuda version ............... 11.8
> torch hip version ................ None
> nvcc version ..................... 11.8
> deepspeed wheel compiled w. ...... torch 1.13, cuda 11.8
> shared memory (/dev/shm) size .... 251.61 GB
> **** Git info for Megatron: git_hash=379cb16 git_branch=main ****
> using world size: 1, data-parallel-size: 1, tensor-model-parallel size: 1, pipeline-model-parallel size: 1
> using torch.float16 for parameters ...
> ------------------------ arguments ------------------------
>   accumulate_allreduce_grads_in_fp32 .............. False
>   adam_beta1 ...................................... 0.9
>   adam_beta2 ...................................... 0.999
>   adam_eps ........................................ 1e-08
>   add_bias_linear ................................. True
>   add_position_embedding .......................... True
>   adlr_autoresume ................................. False
>   adlr_autoresume_interval ........................ 1000
>   apply_layernorm_1p .............................. False
>   apply_query_key_layer_scaling ................... True
>   apply_residual_connection_post_layernorm ........ False
>   async_tensor_model_parallel_allreduce ........... True
>   attention_dropout ............................... 0.1
>   attention_softmax_in_fp32 ....................... False
>   barrier_with_L1_time ............................ True
>   bert_binary_head ................................ True
>   bert_embedder_type .............................. megatron
>   bert_load ....................................... None
>   bf16 ............................................ False
>   bias_dropout_fusion ............................. True
>   bias_gelu_fusion ................................ True
>   biencoder_projection_dim ........................ 0
>   biencoder_shared_query_context_model ............ False
>   block_data_path ................................. None
>   checkpoint_activations .......................... True
>   checkpoint_in_cpu ............................... False
>   checkpoint_num_layers ........................... 1
>   classes_fraction ................................ 1.0
>   clip_grad ....................................... 1.0
>   compression_training ............................ False
>   consumed_train_samples .......................... 0
>   consumed_train_tokens ........................... 0
>   consumed_valid_samples .......................... 0
>   contigious_checkpointing ........................ False
>   cpu_optimizer ................................... True
>   cpu_torch_adam .................................. False
>   create_moe_param_group .......................... False
>   curriculum_learning_legacy ...................... False
>   custom_token_counting ........................... False
>   data_efficiency_curriculum_learning ............. False
>   data_impl ....................................... mmap
>   data_parallel_random_init ....................... False
>   data_parallel_size .............................. 1
>   data_path ....................................... ['/lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document']
>   data_per_class_fraction ......................... 1.0
>   data_sharding ................................... True
>   dataloader_type ................................. single
>   DDP_impl ........................................ local
>   decoder_num_layers .............................. None
>   decoder_seq_length .............................. None
>   deepscale ....................................... False
>   deepscale_config ................................ None
>   deepspeed ....................................... True
>   deepspeed_activation_checkpointing .............. True
>   deepspeed_config ................................ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/ds_config-gpt.json
>   deepspeed_mpi ................................... True
>   dino_bottleneck_size ............................ 256
>   dino_freeze_last_layer .......................... 1
>   dino_head_hidden_size ........................... 2048
>   dino_local_crops_number ......................... 10
>   dino_local_img_size ............................. 96
>   dino_norm_last_layer ............................ False
>   dino_teacher_temp ............................... 0.07
>   dino_warmup_teacher_temp ........................ 0.04
>   dino_warmup_teacher_temp_epochs ................. 30
>   distribute_checkpointed_activations ............. False
>   distribute_saved_activations .................... False
>   distributed_backend ............................. nccl
>   distributed_timeout_minutes ..................... 10
>   ds_inference .................................... False
>   ds_pipeline_enabled ............................. False
>   embedding_path .................................. None
>   empty_unused_memory_level ....................... 0
>   enable_expert_tensor_parallelism ................ False
>   encoder_num_layers .............................. 12
>   encoder_seq_length .............................. 1024
>   end_weight_decay ................................ 0.01
>   eod_mask_loss ................................... False
>   eval_interval ................................... 1000
>   eval_iters ...................................... 1
>   evidence_data_path .............................. None
>   exit_duration_in_mins ........................... None
>   exit_interval ................................... None
>   exit_on_missing_checkpoint ...................... False
>   exit_signal_handler ............................. False
>   expert_interval ................................. 2
>   ffn_hidden_size ................................. 3072
>   finetune ........................................ False
>   fp16 ............................................ True
>   fp16_lm_cross_entropy ........................... False
>   fp32_residual_connection ........................ False
>   fp8_amax_compute_algo ........................... most_recent
>   fp8_amax_history_len ............................ 1
>   fp8_e4m3 ........................................ False
>   fp8_hybrid ...................................... False
>   fp8_interval .................................... 1
>   fp8_margin ...................................... 0
>   fp8_wgrad ....................................... True
>   global_batch_size ............................... 32
>   gradient_accumulation_fusion .................... True
>   head_lr_mult .................................... 1.0
>   hidden_dropout .................................. 0.1
>   hidden_size ..................................... 768
>   hidden_size_teacher ............................. None
>   hysteresis ...................................... 2
>   ict_head_size ................................... None
>   ict_load ........................................ None
>   img_h ........................................... 224
>   img_w ........................................... 224
>   indexer_batch_size .............................. 128
>   indexer_log_interval ............................ 1000
>   inference ....................................... False
>   inference_batch_times_seqlen_threshold .......... 512
>   init_method_std ................................. 0.02
>   init_method_xavier_uniform ...................... False
>   initial_loss_scale .............................. 4294967296
>   iter_per_epoch .................................. 1250
>   kd .............................................. False
>   kd_alpha_ce ..................................... 1
>   kd_beta_ce ...................................... 1
>   kd_temp ......................................... 1.0
>   kv_channels ..................................... 48
>   layernorm_epsilon ............................... 1e-05
>   lazy_mpu_init ................................... None
>   load ............................................ None
>   load_teacher .................................... None
>   local_rank ...................................... None
>   log_batch_size_to_tensorboard ................... False
>   log_interval .................................... 1
>   log_learning_rate_to_tensorboard ................ True
>   log_loss_scale_to_tensorboard ................... True
>   log_memory_to_tensorboard ....................... False
>   log_num_zeros_in_grad ........................... False
>   log_optimizer_states_to_tensorboard ............. False
>   log_params_norm ................................. False
>   log_timers_to_tensorboard ....................... True
>   log_validation_ppl_to_tensorboard ............... False
>   log_world_size_to_tensorboard ................... False
>   loss_scale ...................................... None
>   loss_scale_window ............................... 1000
>   lr .............................................. 0.00015
>   lr_decay_iters .................................. 320000
>   lr_decay_samples ................................ None
>   lr_decay_style .................................. cosine
>   lr_decay_tokens ................................. None
>   lr_warmup_fraction .............................. 0.01
>   lr_warmup_iters ................................. 0
>   lr_warmup_samples ............................... 0
>   lr_warmup_tokens ................................ None
>   make_vocab_size_divisible_by .................... 128
>   mask_factor ..................................... 1.0
>   mask_prob ....................................... 0.15
>   mask_type ....................................... random
>   masked_softmax_fusion ........................... True
>   max_position_embeddings ......................... 1024
>   max_tokens_to_oom ............................... 12000
>   memory_centric_tiled_linear ..................... False
>   merge_file ...................................... /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-merges.txt
>   micro_batch_size ................................ 4
>   min_loss_scale .................................. 1.0
>   min_lr .......................................... 1e-05
>   mlp_type ........................................ standard
>   mmap_warmup ..................................... False
>   moe_eval_capacity_factor ........................ 1.0
>   moe_expert_parallel_size ........................ 1
>   moe_loss_coeff .................................. 0.1
>   moe_min_capacity ................................ 4
>   moe_token_dropping .............................. True
>   moe_train_capacity_factor ....................... 1.0
>   mos ............................................. False
>   no_load_lr_state ................................ False
>   no_load_optim ................................... None
>   no_load_rng ..................................... None
>   no_persist_layer_norm ........................... False
>   no_pipeline_parallel ............................ True
>   no_save_optim ................................... None
>   no_save_rng ..................................... None
>   num_attention_heads ............................. 16
>   num_attention_heads_teacher ..................... None
>   num_channels .................................... 3
>   num_classes ..................................... 1000
>   num_experts ..................................... [1]
>   num_experts_switch .............................. None
>   num_experts_teacher ............................. [1]
>   num_layers ...................................... 12
>   num_layers_per_virtual_pipeline_stage ........... None
>   num_layers_teacher .............................. None
>   num_workers ..................................... 1
>   onnx_safe ....................................... None
>   openai_gelu ..................................... False
>   optimizer ....................................... adam
>   output_bert_embeddings .......................... False
>   override_opt_param_scheduler .................... True
>   params_dtype .................................... torch.float16
>   partition_activations ........................... False
>   patch_dim ....................................... 16
>   perform_initialization .......................... True
>   pipeline_model_parallel_size .................... 1
>   pipeline_model_parallel_split_rank .............. None
>   profile_backward ................................ False
>   query_in_block_prob ............................. 0.1
>   rampup_batch_size ............................... None
>   random_ltd ...................................... False
>   rank ............................................ 0
>   recompute_activations ........................... False
>   recompute_granularity ........................... None
>   recompute_method ................................ None
>   recompute_num_layers ............................ 1
>   remote_device ................................... none
>   reset_attention_mask ............................ False
>   reset_iteration ................................. False
>   reset_position_ids .............................. False
>   retriever_report_topk_accuracies ................ []
>   retriever_score_scaling ......................... False
>   retriever_seq_length ............................ 256
>   retro_add_retriever ............................. False
>   retro_cyclic_train_iters ........................ None
>   retro_encoder_attention_dropout ................. 0.1
>   retro_encoder_hidden_dropout .................... 0.1
>   retro_encoder_layers ............................ 2
>   retro_num_neighbors ............................. 2
>   retro_num_retrieved_chunks ...................... 2
>   retro_return_doc_ids ............................ False
>   retro_workdir ................................... None
>   return_data_index ............................... False
>   rotary_percent .................................. 1.0
>   sample_rate ..................................... 1.0
>   save ............................................ None
>   save_interval ................................... 1000
>   scatter_gather_tensors_in_pipeline .............. True
>   scattered_embeddings ............................ False
>   seed ............................................ 19855
>   seq_length ...................................... 1024
>   sequence_parallel ............................... False
>   sequence_parallel_size .......................... 1
>   sgd_momentum .................................... 0.9
>   short_seq_prob .................................. 0.1
>   split ........................................... 949,50,1
>   split_transformers .............................. False
>   squared_relu .................................... False
>   standalone_embedding_stage ...................... False
>   start_weight_decay .............................. 0.01
>   swiglu .......................................... False
>   swin_backbone_type .............................. tiny
>   synchronize_each_layer .......................... False
>   tensor_model_parallel_size ...................... 1
>   tensorboard_dir ................................. /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/tensorboard
>   tensorboard_log_interval ........................ 1
>   tensorboard_queue_size .......................... 1000
>   test_data_path .................................. None
>   tile_factor ..................................... 1
>   timing_log_level ................................ 0
>   timing_log_option ............................... minmax
>   titles_data_path ................................ None
>   tokenizer_model ................................. None
>   tokenizer_type .................................. GPT2BPETokenizer
>   topk ............................................ 1
>   train_data_exact_num_epochs ..................... None
>   train_data_path ................................. None
>   train_doc_idx_path .............................. None
>   train_idx_path .................................. None
>   train_iters ..................................... 5
>   train_sample_idx_path ........................... None
>   train_samples ................................... None
>   train_shuffle_idx_path .......................... None
>   train_tokens .................................... None
>   transformer_impl ................................ local
>   transformer_pipeline_model_parallel_size ........ 1
>   untie_embeddings_and_output_weights ............. False
>   use_checkpoint_args ............................. False
>   use_checkpoint_opt_param_scheduler .............. False
>   use_contiguous_buffers_in_ddp ................... False
>   use_cpu_initialization .......................... None
>   use_distributed_optimizer ....................... False
>   use_flash_attn .................................. False
>   use_one_sent_docs ............................... False
>   use_pin_memory .................................. False
>   use_ring_exchange_p2p ........................... False
>   use_rotary_position_embeddings .................. False
>   use_tutel ....................................... False
>   valid_data_path ................................. None
>   variable_seq_lengths ............................ False
>   virtual_pipeline_model_parallel_size ............ None
>   vision_backbone_type ............................ vit
>   vision_pretraining .............................. False
>   vision_pretraining_type ......................... classify
>   vocab_extra_ids ................................. 0
>   vocab_file ...................................... /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/gpt2-vocab.json
>   vocab_size ...................................... None
>   weight_decay .................................... 0.01
>   weight_decay_incr_style ......................... constant
>   world_size ...................................... 1
>   zero_allgather_bucket_size ...................... 0.0
>   zero_contigious_gradients ....................... False
>   zero_reduce_bucket_size ......................... 0.0
>   zero_reduce_scatter ............................. False
>   zero_stage ...................................... 1
> -------------------- end of arguments ---------------------
> setting number of micro-batches to constant 8
> > building GPT2BPETokenizer tokenizer ...
>  > padded vocab (size: 50257) with 47 dummy tokens (new size: 50304)
> > setting tensorboard ...
> torch distributed is already initialized, skipping initialization ...
> > initialized tensor model parallel with size 1
> > initialized pipeline model parallel with size 1
> > setting random seeds to 19855 ...
> > initializing model parallel cuda seeds on global rank 0, model parallel rank 0, and data parallel rank 0 with model parallel seed: 22573 and data parallel seed: 19855
> > compiling dataset index builder ...
> make: Entering directory '/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/data'
> make: Nothing to be done for 'default'.
> make: Leaving directory '/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/data'
> >>> done with dataset index builder. Compilation time: 0.053 seconds
> > compiling and loading fused kernels ...
> Detected CUDA files, patching ldflags
> Emitting ninja build file /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/fused_kernels/build/build.ninja...
> Building extension module scaled_upper_triang_masked_softmax_cuda...
> Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
> ninja: no work to do.
> Loading extension module scaled_upper_triang_masked_softmax_cuda...
> Detected CUDA files, patching ldflags
> Emitting ninja build file /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/fused_kernels/build/build.ninja...
> Building extension module scaled_masked_softmax_cuda...
> Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
> ninja: no work to do.
> Loading extension module scaled_masked_softmax_cuda...
> Detected CUDA files, patching ldflags
> Emitting ninja build file /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/fused_kernels/build/build.ninja...
> Building extension module scaled_softmax_cuda...
> Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
> ninja: no work to do.
> Loading extension module scaled_softmax_cuda...
> >>> done with compiling and loading fused kernels. Compilation time: 1.624 seconds
> time to initialize megatron (seconds): 10.553
> [after megatron is initialized] datetime: 2023-08-08 16:28:36
> building GPT model ...
> [2023-08-08 16:28:36,668] [INFO] [utils.py:803:see_memory_usage] Before Building Model
> [2023-08-08 16:28:36,669] [INFO] [utils.py:804:see_memory_usage] MA 0.0 GB         Max_MA 0.4 GB         CA 0.0 GB         Max_CA 0 GB
> [2023-08-08 16:28:36,669] [INFO] [utils.py:811:see_memory_usage] CPU Virtual Memory:  used = 14.29 GB, percent = 2.8%
> wandb: logging graph, to disable use `wandb.watch(log_graph=False)`
> [2023-08-08 16:28:36,846] [INFO] [utils.py:803:see_memory_usage] After Building Model
> [2023-08-08 16:28:36,846] [INFO] [utils.py:804:see_memory_usage] MA 0.24 GB         Max_MA 0.24 GB         CA 0.25 GB         Max_CA 0 GB
> [2023-08-08 16:28:36,847] [INFO] [utils.py:811:see_memory_usage] CPU Virtual Memory:  used = 14.31 GB, percent = 2.8%
> 
>  ------------------------
> num of parameters 124475904
> ------------------------
> 
>  > number of parameters on (tensor, pipeline) model parallel rank (0, 0): 124475904
> [2023-08-08 16:28:38,027] [WARNING] [cpu_adam.py:84:__init__] FP16 params for CPUAdam may not work on AMD CPUs
> Adam Optimizer #0 is created with AVX2 arithmetic capability.
> Config: alpha=0.000150, betas=(0.900000, 0.999000), weight_decay=0.010000, adam_w=1
> > learning rate decay style: cosine
> DeepSpeed is enabled.
> [2023-08-08 16:28:38,715] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed info: version=0.10.1+57a27b08, git-hash=57a27b08, git-branch=master
> [2023-08-08 16:28:38,814] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed Flops Profiler Enabled: True
> [2023-08-08 16:28:38,815] [INFO] [logging.py:96:log_dist] [Rank 0] Removing param_group that has no 'params' in the client Optimizer
> [2023-08-08 16:28:38,815] [INFO] [logging.py:96:log_dist] [Rank 0] Using client Optimizer as basic optimizer
> [2023-08-08 16:28:38,819] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed Basic Optimizer = DeepSpeedCPUAdam
> [2023-08-08 16:28:38,819] [INFO] [utils.py:54:is_zero_supported_optimizer] Checking ZeRO support for optimizer=DeepSpeedCPUAdam type=<class 'deepspeed.ops.adam.cpu_adam.DeepSpeedCPUAdam'>
> [2023-08-08 16:28:38,819] [INFO] [logging.py:96:log_dist] [Rank 0] Creating torch.float16 ZeRO stage 1 optimizer
> [2023-08-08 16:28:38,819] [INFO] [stage_1_and_2.py:139:__init__] Reduce bucket size 500,000,000
> [2023-08-08 16:28:38,820] [INFO] [stage_1_and_2.py:140:__init__] Allgather bucket size 500000000
> [2023-08-08 16:28:38,820] [INFO] [stage_1_and_2.py:141:__init__] CPU Offload: True
> [2023-08-08 16:28:38,820] [INFO] [stage_1_and_2.py:142:__init__] Round robin gradient partitioning: False
> Rank: 0 partition count [1, 1] and sizes[(124354560, False), (121344, False)]
> [2023-08-08 16:28:39,220] [INFO] [utils.py:803:see_memory_usage] Before initializing optimizer states
> [2023-08-08 16:28:39,221] [INFO] [utils.py:804:see_memory_usage] MA 0.3 GB         Max_MA 0.3 GB         CA 0.31 GB         Max_CA 0 GB
> [2023-08-08 16:28:39,221] [INFO] [utils.py:811:see_memory_usage] CPU Virtual Memory:  used = 17.02 GB, percent = 3.4%
> [2023-08-08 16:28:39,650] [INFO] [utils.py:803:see_memory_usage] After initializing optimizer states
> [2023-08-08 16:28:39,651] [INFO] [utils.py:804:see_memory_usage] MA 0.3 GB         Max_MA 0.3 GB         CA 0.31 GB         Max_CA 0 GB
> [2023-08-08 16:28:39,652] [INFO] [utils.py:811:see_memory_usage] CPU Virtual Memory:  used = 18.46 GB, percent = 3.7%
> [2023-08-08 16:28:39,652] [INFO] [stage_1_and_2.py:511:__init__] optimizer state initialized
> [2023-08-08 16:28:39,790] [INFO] [utils.py:803:see_memory_usage] After initializing ZeRO optimizer
> [2023-08-08 16:28:39,790] [INFO] [utils.py:804:see_memory_usage] MA 0.3 GB         Max_MA 0.3 GB         CA 0.31 GB         Max_CA 0 GB
> [2023-08-08 16:28:39,791] [INFO] [utils.py:811:see_memory_usage] CPU Virtual Memory:  used = 18.46 GB, percent = 3.7%
> [2023-08-08 16:28:39,794] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed Final Optimizer = DeepSpeedCPUAdam
> [2023-08-08 16:28:39,794] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed using configured LR scheduler = WarmupLR
> [2023-08-08 16:28:39,794] [INFO] [logging.py:96:log_dist] [Rank 0] DeepSpeed LR Scheduler = <deepspeed.runtime.lr_schedules.WarmupLR object at 0x7f58c1310160>
> [2023-08-08 16:28:39,794] [INFO] [logging.py:96:log_dist] [Rank 0] step=0, skipped=0, lr=[0.0, 0.0], mom=[(0.9, 0.999), (0.9, 0.999)]
> [2023-08-08 16:28:39,794] [INFO] [config.py:960:print] DeepSpeedEngine configuration:
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   activation_checkpointing_config  {
>     "partition_activations": false,
>     "contiguous_memory_optimization": false,
>     "cpu_checkpointing": false,
>     "number_checkpoints": null,
>     "synchronize_checkpoint_boundary": false,
>     "profile": false
> }
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   aio_config ................... {'block_size': 1048576, 'queue_depth': 8, 'thread_count': 1, 'single_submit': False, 'overlap_events': True}
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   amp_enabled .................. False
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   amp_params ................... False
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   autotuning_config ............ {
>     "enabled": false,
>     "start_step": null,
>     "end_step": null,
>     "metric_path": null,
>     "arg_mappings": null,
>     "metric": "throughput",
>     "model_info": null,
>     "results_dir": "autotuning_results",
>     "exps_dir": "autotuning_exps",
>     "overwrite": true,
>     "fast": true,
>     "start_profile_step": 3,
>     "end_profile_step": 5,
>     "tuner_type": "gridsearch",
>     "tuner_early_stopping": 5,
>     "tuner_num_trials": 50,
>     "model_info_path": null,
>     "mp_size": 1,
>     "max_train_batch_size": null,
>     "min_train_batch_size": 1,
>     "max_train_micro_batch_size_per_gpu": 1.024000e+03,
>     "min_train_micro_batch_size_per_gpu": 1,
>     "num_tuning_micro_batch_sizes": 3
> }
> [2023-08-08 16:28:39,795] [INFO] [config.py:964:print]   bfloat16_enabled ............. False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   checkpoint_parallel_write_pipeline  False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   checkpoint_tag_validation_enabled  True
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   checkpoint_tag_validation_fail  False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   comms_config ................. <deepspeed.comm.config.DeepSpeedCommsConfig object at 0x7f58c13104f0>
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   communication_data_type ...... None
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   compression_config ........... {'weight_quantization': {'shared_parameters': {'enabled': False, 'quantizer_kernel': False, 'schedule_offset': 0, 'quantize_groups': 1, 'quantize_verbose': False, 'quantization_type': 'symmetric', 'quantize_weight_in_forward': False, 'rounding': 'nearest', 'fp16_mixed_quantize': False, 'quantize_change_ratio': 0.001}, 'different_groups': {}}, 'activation_quantization': {'shared_parameters': {'enabled': False, 'quantization_type': 'symmetric', 'range_calibration': 'dynamic', 'schedule_offset': 1000}, 'different_groups': {}}, 'sparse_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'row_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'head_pruning': {'shared_parameters': {'enabled': False, 'method': 'topk', 'schedule_offset': 1000}, 'different_groups': {}}, 'channel_pruning': {'shared_parameters': {'enabled': False, 'method': 'l1', 'schedule_offset': 1000}, 'different_groups': {}}, 'layer_reduction': {'enabled': False}}
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   curriculum_enabled_legacy .... False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   curriculum_params_legacy ..... False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   data_efficiency_config ....... {'enabled': False, 'seed': 1234, 'data_sampling': {'enabled': False, 'num_epochs': 1000, 'num_workers': 0, 'curriculum_learning': {'enabled': False}}, 'data_routing': {'enabled': False, 'random_ltd': {'enabled': False, 'layer_token_lr_schedule': {'enabled': False}}}}
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   data_efficiency_enabled ...... False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   dataloader_drop_last ......... False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   disable_allgather ............ False
> [2023-08-08 16:28:39,796] [INFO] [config.py:964:print]   dump_state ................... False
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   dynamic_loss_scale_args ...... {'init_scale': 4096, 'scale_window': 1000, 'delayed_shift': 2, 'consecutive_hysteresis': False, 'min_scale': 1}
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_enabled ........... False
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_gas_boundary_resolution  1
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_layer_name ........ bert.encoder.layer
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_layer_num ......... 0
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_max_iter .......... 100
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_stability ......... 1e-06
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_tol ............... 0.01
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   eigenvalue_verbose ........... False
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   elasticity_enabled ........... False
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   flops_profiler_config ........ {
>     "enabled": true,
>     "recompute_fwd_factor": 0.0,
>     "profile_step": 1,
>     "module_depth": -1,
>     "top_modules": 3,
>     "detailed": true,
>     "output_file": null
> }
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   fp16_auto_cast ............... False
> [2023-08-08 16:28:39,797] [INFO] [config.py:964:print]   fp16_enabled ................. True
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   fp16_master_weights_and_gradients  False
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   global_rank .................. 0
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   grad_accum_dtype ............. None
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   gradient_accumulation_steps .. 1
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   gradient_clipping ............ 0.0
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   gradient_predivide_factor .... 1.0
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   hybrid_engine ................ enabled=False max_out_tokens=512 inference_tp_size=1 release_inference_cache=False pin_parameters=True tp_gather_partition_size=8
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   initial_dynamic_scale ........ 4096
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   load_universal_checkpoint .... False
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   loss_scale ................... 0
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   memory_breakdown ............. False
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   mics_hierarchial_params_gather  False
> [2023-08-08 16:28:39,798] [INFO] [config.py:964:print]   mics_shard_size .............. -1
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   monitor_config ............... tensorboard=TensorBoardConfig(enabled=False, output_path='', job_name='DeepSpeedJobName') wandb=WandbConfig(enabled=True, group='megatron-DS0', team=None, project='megatron-DS') csv_monitor=CSVConfig(enabled=False, output_path='', job_name='DeepSpeedJobName') enabled=True
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   nebula_config ................ {
>     "enabled": false,
>     "persistent_storage_path": null,
>     "persistent_time_interval": 100,
>     "num_of_version_in_retention": 2,
>     "enable_nebula_load": true,
>     "load_path": null
> }
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   optimizer_legacy_fusion ...... False
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   optimizer_name ............... adam
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   optimizer_params ............. {'lr': 0.001, 'betas': [0.8, 0.999], 'eps': 1e-08, 'weight_decay': 3e-07}
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   pipeline ..................... {'stages': 'auto', 'partition': 'best', 'seed_layers': False, 'activation_checkpoint_interval': 0}
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   pld_enabled .................. False
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   pld_params ................... False
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   prescale_gradients ........... False
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   scheduler_name ............... WarmupLR
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   scheduler_params ............. {'warmup_min_lr': 0, 'warmup_max_lr': 0.001, 'warmup_num_steps': 1000}
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   sparse_attention ............. None
> [2023-08-08 16:28:39,799] [INFO] [config.py:964:print]   sparse_gradients_enabled ..... False
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   steps_per_print .............. 1
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   train_batch_size ............. 4
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   train_micro_batch_size_per_gpu  4
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   use_node_local_storage ....... False
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   wall_clock_breakdown ......... True
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   world_size ................... 1
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   zero_allow_untested_optimizer  False
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   zero_config .................. stage=1 contiguous_gradients=True reduce_scatter=True reduce_bucket_size=500,000,000 allgather_partitions=True allgather_bucket_size=500000000 overlap_comm=True load_from_fp32_weights=True elastic_checkpoint=False offload_param=None offload_optimizer=DeepSpeedZeroOffloadOptimizerConfig(device='cpu', nvme_path=None, buffer_count=4, pin_memory=True, pipeline=False, pipeline_read=False, pipeline_write=False, fast_init=False) sub_group_size=1,000,000,000 cpu_offload_param=None cpu_offload_use_pin_memory=None cpu_offload=None prefetch_bucket_size=50,000,000 param_persistence_threshold=100,000 model_persistence_threshold=sys.maxsize max_live_parameters=1,000,000,000 max_reuse_distance=1,000,000,000 gather_16bit_weights_on_model_save=False stage3_gather_fp16_weights_on_model_save=False ignore_unused_parameters=True legacy_stage1=False round_robin_gradients=False zero_hpz_partition_size=1 zero_quantized_weights=False zero_quantized_gradients=False mics_shard_size=-1 mics_hierarchical_params_gather=False memory_efficient_linear=True override_module_apply=True
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   zero_enabled ................. True
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   zero_force_ds_cpu_optimizer .. True
> [2023-08-08 16:28:39,800] [INFO] [config.py:964:print]   zero_optimization_stage ...... 1
> [2023-08-08 16:28:39,801] [INFO] [config.py:950:print_user_config]   json = {
>     "train_micro_batch_size_per_gpu": 4,
>     "gradient_accumulation_steps": 1,
>     "steps_per_print": 1,
>     "wall_clock_breakdown": true,
>     "zero_force_ds_cpu_optimizer": true,
>     "zero_optimization": {
>         "stage": 1,
>         "allgather_partitions": true,
>         "reduce_scatter": true,
>         "allgather_bucket_size": 5.000000e+08,
>         "overlap_comm": true,
>         "contiguous_gradients": true,
>         "offload_optimizer": {
>             "device": "cpu",
>             "buffer_count": 4,
>             "pipeline_read": false,
>             "pipeline_write": false,
>             "pin_memory": true
>         }
>     },
>     "optimizer": {
>         "type": "Adam",
>         "params": {
>             "lr": 0.001,
>             "betas": [0.8, 0.999],
>             "eps": 1e-08,
>             "weight_decay": 3e-07
>         }
>     },
>     "scheduler": {
>         "type": "WarmupLR",
>         "params": {
>             "warmup_min_lr": 0,
>             "warmup_max_lr": 0.001,
>             "warmup_num_steps": 1000
>         }
>     },
>     "fp16": {
>         "enabled": true,
>         "initial_scale_power": 12
>     },
>     "flops_profiler": {
>         "enabled": true,
>         "profile_step": 1,
>         "module_depth": -1,
>         "top_modules": 3,
>         "detailed": true,
>         "output_file": null
>     },
>     "comms_logger": {
>         "enabled": true,
>         "verbose": false,
>         "prof_all": false,
>         "debug": false
>     },
>     "wandb": {
>         "enabled": true,
>         "group": "megatron-DS0",
>         "project": "megatron-DS"
>     }
> }
> [after model, optimizer, and learning rate scheduler are built] datetime: 2023-08-08 16:28:39
> > building train, validation, and test datasets ...
>  > datasets target sizes (minimum size):
>     train:      160
>     validation: 32
>     test:       32
> > building train, validation, and test datasets for GPT ...
> Single data path provided for train, valid & test
>  > building dataset index ...
>     reading sizes...
>     reading pointers...
>     reading document index...
>     creating numpy buffer of mmap...
>     creating memory view of numpy buffer...
>  > finished creating indexed dataset in 0.002093 seconds
>     number of documents: 17868
>  > dataset split:
>     train:
>      document indices in [0, 16957) total of 16957 documents
>     validation:
>      document indices in [16957, 17850) total of 893 documents
>     test:
>      document indices in [17850, 17868) total of 18 documents
>  > WARNING: could not find index map files, building the indices on rank 0 ...
>  > only one epoch required, setting separate_last_epoch to False
>  > elasped time to build and save doc-idx mapping (seconds): 0.002110
>     using:
>      number of documents:       16957
>      number of epochs:          1
>      sequence length:           1024
>      total number of samples:   1495435
>  > elasped time to build and save sample-idx mapping (seconds): 0.088466
>  > building shuffle index with split [0, 1495435) and [1495435, 1495435) ...
>  > elasped time to build and save shuffle-idx mapping (seconds): 0.031370
>  > loading doc-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_train_indexmap_160ns_1024sl_19855s_doc_idx.npy
>  > loading sample-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_train_indexmap_160ns_1024sl_19855s_sample_idx.npy
>  > loading shuffle-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_train_indexmap_160ns_1024sl_19855s_shuffle_idx.npy
>     loaded indexed file in 0.004 seconds
>     total number of samples: 1495436
>     total number of epochs: 1
>  > WARNING: could not find index map files, building the indices on rank 0 ...
>  > only one epoch required, setting separate_last_epoch to False
>  > elasped time to build and save doc-idx mapping (seconds): 0.001504
>     using:
>      number of documents:       893
>      number of epochs:          1
>      sequence length:           1024
>      total number of samples:   77807
>  > elasped time to build and save sample-idx mapping (seconds): 0.001795
>  > building shuffle index with split [0, 77807) and [77807, 77807) ...
>  > elasped time to build and save shuffle-idx mapping (seconds): 0.003089
>  > loading doc-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_valid_indexmap_32ns_1024sl_19855s_doc_idx.npy
>  > loading sample-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_valid_indexmap_32ns_1024sl_19855s_sample_idx.npy
>  > loading shuffle-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_valid_indexmap_32ns_1024sl_19855s_shuffle_idx.npy
>     loaded indexed file in 0.002 seconds
>     total number of samples: 77808
>     total number of epochs: 1
>  > WARNING: could not find index map files, building the indices on rank 0 ...
>  > only one epoch required, setting separate_last_epoch to False
>  > elasped time to build and save doc-idx mapping (seconds): 0.001711
>     using:
>      number of documents:       18
>      number of epochs:          1
>      sequence length:           1024
>      total number of samples:   2188
>  > elasped time to build and save sample-idx mapping (seconds): 0.001569
>  > building shuffle index with split [0, 2188) and [2188, 2188) ...
>  > elasped time to build and save shuffle-idx mapping (seconds): 0.001628
>  > loading doc-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_test_indexmap_32ns_1024sl_19855s_doc_idx.npy
>  > loading sample-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_test_indexmap_32ns_1024sl_19855s_sample_idx.npy
>  > loading shuffle-idx mapping from /lus/grand/projects/datascience/foremans/locations/polaris/projects/saforem2/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_document_test_indexmap_32ns_1024sl_19855s_shuffle_idx.npy
>     loaded indexed file in 0.003 seconds
>     total number of samples: 2189
>     total number of epochs: 1
> > finished creating GPT datasets ...
> [after dataloaders are built] datetime: 2023-08-08 16:29:10
> done with setup ...
> /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/distributed/distributed_c10d.py:2387: UserWarning: torch.distributed._all_gather_base is a private function and will be deprecated. Please use torch.distributed.all_gather_into_tensor instead.
>   warnings.warn(
> (min, max) time across ranks (ms):
>     model-and-optimizer-setup ......................: (3283.61, 3283.61)
>     train/valid/test-data-iterators-setup ..........: (30231.95, 30231.95)
> training ...
> [before the start of training step] datetime: 2023-08-08 16:29:10
> wandb: WARNING Step cannot be set when using syncing with tensorboard. Please log your step values as a metric such as 'global_step'
> [2023-08-08 16:29:11,600] [INFO] [logging.py:96:log_dist] [Rank 0] time (ms) | optimizer_allgather: 1.05 | optimizer_gradients: 19.94 | optimizer_step: 77.19
> Traceback (most recent call last):
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py", line 2033, in _take_model_step
>     self.lr_scheduler.step(**(lr_kwargs or {}))
> TypeError: WarmupLR.step() got an unexpected keyword argument 'increment'
> 
> During handling of the above exception, another exception occurred:
> 
> Traceback (most recent call last):
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/pretrain_gpt.py", line 477, in <module>
>     main()
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/pretrain_gpt.py", line 460, in main
>     pretrain(
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/training.py", line 212, in pretrain
>     iteration = train(forward_step_func,
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/training.py", line 1416, in train
>     train_step(forward_step_func,
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/megatron/training.py", line 733, in train_step
>     model[0].step(lr_kwargs={'increment': increment})
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py", line 2084, in step
>     self._take_model_step(lr_kwargs)
>   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS-Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py", line 2038, in _take_model_step
>     self.lr_scheduler.step(increment=self.train_batch_size())
> TypeError: WarmupLR.step() got an unexpected keyword argument 'increment'
> ╭─────────────────────────────── Traceback (most recent call last) ────────────────────────────────╮
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py:2 │
> │ 033 in _take_model_step                                                                          │
> │                                                                                                  │
> │   2030 │   │   │   self.compression_scheduler.step()                                             │
> │   2031 │   │   │   if self.lr_scheduler is not None:                                             │
> │   2032 │   │   │   │   try:                                                                      │
> │ ❱ 2033 │   │   │   │   │   self.lr_scheduler.step(**(lr_kwargs or {}))                           │
> │   2034 │   │   │   │   except TypeError:                                                         │
> │   2035 │   │   │   │   │   # XXX Hack to work with Megatron 2.0 and DeepSpeed pipelines.         │
> │   2036 │   │   │   │   │   # We don't currently have a way to specify lr_kwargs from             │
> ╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
> TypeError: WarmupLR.step() got an unexpected keyword argument 'increment'
> 
> During handling of the above exception, another exception occurred:
> 
> ╭─────────────────────────────── Traceback (most recent call last) ────────────────────────────────╮
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/pretrain_gpt.py:477 in <module>                                                     │
> │                                                                                                  │
> │   474                                                                                            │
> │   475 if __name__ == "__main__":                                                                 │
> │   476 │   wandb.require(experiment='service')                                                    │
> │ ❱ 477 │   main()                                                                                 │
> │   478                                                                                            │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/pretrain_gpt.py:460 in main                                                         │
> │                                                                                                  │
> │   457 │   import deepspeed.comm as dist                                                          │
> │   458 │   git_ds_info()                                                                          │
> │   459 │   t0 = time.time()                                                                       │
> │ ❱ 460 │   pretrain(                                                                              │
> │   461 │   │   train_valid_test_datasets_provider,                                                │
> │   462 │   │   model_provider,                                                                    │
> │   463 │   │   ModelType.encoder_or_decoder,                                                      │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/megatron/training.py:212 in pretrain                                                │
> │                                                                                                  │
> │    209 │   │   print_rank_0("retro cyclic train iters : %d" % args.train_iters)                  │
> │    210 │                                                                                         │
> │    211 │   if args.do_train and args.train_iters > 0:                                            │
> │ ❱  212 │   │   iteration = train(forward_step_func,                                              │
> │    213 │   │   │   │   │   │     model, optimizer, opt_param_scheduler,                          │
> │    214 │   │   │   │   │   │     train_data_iterator, valid_data_iterator,                       │
> │    215 │   │   │   │   │   │     process_non_loss_data_func, wbrun=wbrun)                        │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/megatron/training.py:1416 in train                                                  │
> │                                                                                                  │
> │   1413 │   │   │   │   │   args.curr_iteration + 1)                                              │
> │   1414 │   │   args.curr_iteration = iteration                                                   │
> │   1415 │   │   loss_dict, skipped_iter, grad_norm, num_zeros_in_grad = \                         │
> │ ❱ 1416 │   │   │   train_step(forward_step_func,                                                 │
> │   1417 │   │   │   │   │   train_data_iterator,                                                  │
> │   1418 │   │   │   │   │   model,                                                                │
> │   1419 │   │   │   │   │   optimizer,                                                            │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/megatron/training.py:733 in train_step                                              │
> │                                                                                                  │
> │    730 │   │   increment = get_num_microbatches() * \                                            │
> │    731 │   │   │   │   │   args.micro_batch_size * \                                             │
> │    732 │   │   │   │   │   args.data_parallel_size                                               │
> │ ❱  733 │   │   model[0].step(lr_kwargs={'increment': increment})                                 │
> │    734 │   │   update_successful = model[0].was_step_applied()                                   │
> │    735 │   else:                                                                                 │
> │    736 │   │   update_successful, grad_norm, num_zeros_in_grad = optimizer.step()                │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py:2 │
> │ 084 in step                                                                                      │
> │                                                                                                  │
> │   2081 │   │   │   │   │   and self.quantizer.any_precision_switch()):                           │
> │   2082 │   │   │   │   self._take_model_step(lr_kwargs, self.block_eigenvalue)                   │
> │   2083 │   │   │   else:                                                                         │
> │ ❱ 2084 │   │   │   │   self._take_model_step(lr_kwargs)                                          │
> │   2085 │   │   │                                                                                 │
> │   2086 │   │   │   report_progress = self.global_rank == 0 if self.global_rank else True         │
> │   2087                                                                                           │
> │                                                                                                  │
> │ /lus/grand/projects/datascience/foremans/locations/polaris/projects/zhangsmallshark/Megatron-DS- │
> │ Benchmarking/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/engine.py:2 │
> │ 038 in _take_model_step                                                                          │
> │                                                                                                  │
> │   2035 │   │   │   │   │   # XXX Hack to work with Megatron 2.0 and DeepSpeed pipelines.         │
> │   2036 │   │   │   │   │   # We don't currently have a way to specify lr_kwargs from             │
> │   2037 │   │   │   │   │   # pipe_engine.train_batch()                                           │
> │ ❱ 2038 │   │   │   │   │   self.lr_scheduler.step(increment=self.train_batch_size())             │
> │   2039 │   │                                                                                     │
> │   2040 │   │   if report_progress and (self.global_steps + 1) % self.steps_per_print() == 0:     │
> │   2041 │   │   │   self._report_progress(self.global_steps + 1)                                  │
> ╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
> TypeError: WarmupLR.step() got an unexpected keyword argument 'increment'
> wandb: Waiting for W&B process to finish... (failed 1). Press Control-C to abort syncing.
> wandb:
> wandb: Run history:
> wandb:                     Train/Samples/train_loss ▁
> wandb:                  averaged_loss/averaged_loss ▄▁█▅▆▆█▇
> wandb:                                  global_step ▁
> wandb:                       timers/batch-generator █▁▄▄█▄█▁
> wandb:                          timers/forward_step █▂▃▃▄▃▄▁
> wandb:             timers/model-and-optimizer-setup ▁
> wandb: timers/train/valid/test-data-iterators-setup ▁
> wandb:
> wandb: Run summary:
> wandb:                     Train/Samples/train_loss 10.9231
> wandb:                  averaged_loss/averaged_loss 10.93147
> wandb:                                  global_step 0
> wandb:                       timers/batch-generator 0.05258
> wandb:                          timers/forward_step 0.0711
> wandb:             timers/model-and-optimizer-setup 0.0
> wandb: timers/train/valid/test-data-iterators-setup 0.0
> wandb:
> wandb: 🚀 View run 1kseq-len-new-32global-batch-1GPUs-1MP-1PP-16-28 at: https://wandb.ai/l2hmc-qcd/Megatron-DS1/runs/14ynrmls
> wandb: Synced 6 W&B file(s), 1 media file(s), 3 artifact file(s) and 2 other file(s)
> wandb: Find logs at: ./outputs/gpt_SP_actCkpt_GPT125M_z1_seqlen1024_mp1_pp1_sp1_nl12_hs768_gb32_mb4/tensorboard/wandb/run-20230808_162828-14ynrmls/logs
> 53.83s user 20.39s system 102% cpu 1:12.44s total
> ```
