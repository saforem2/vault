
# GenSLM

## 2023-01-25

> [!DONE]+ SINGLE DEVICE
> ```bash
> $  CUDA_VISIBLE_DEVICES=0 python3 model.py -c settings_template.yaml
> 2023-01-25 21:58:01.068233: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  SSE3 SSE4.1 SSE4.2 AVX AVX2 FMA
> To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
> /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/saforem2/genslm/genslm/config.py:234: UserWarning: Both checkpoint_every_n_train_steps and checkpoint_every_n_epochs are missing in the configuration. PLease specify one of these to log checkpoints.
>   warnings.warn(
> Global seed set to 0
> model.py:561: UserWarning: You are running in compute throughput mode - running for 6 epochs to compute samples per second. No validation or test sets run. No model checkpointing.
>   warnings.warn(
> Number of model parameters: 0
> rank='0', local_rank='0', slurm_procid=None, jsm_namespace=None, node_rank=None
> GPU available: True, used: True
> TPU available: False, using: 0 TPU cores
> IPU available: False, using: 0 IPUs
> HPU available: False, using: 0 HPUs
> Global seed set to 0
> initializing deepspeed distributed: GLOBAL_RANK: 0, MEMBER: 1/1
> Enabling DeepSpeed FP16.
> LOCAL_RANK: 0 - CUDA_VISIBLE_DEVICES: [0]
> [2023-01-25 21:58:15,924] [WARNING] [cpu_adam.py:84:__init__] FP16 params for CPUAdam may not work on AMD CPUs
> Parameter Offload: Total persistent parameters: 124928 in 68 params
> 
>   | Name  | Type               | Params
> ---------------------------------------------
> 0 | model | GPTNeoXForCausalLM | 0
> ---------------------------------------------
> 0         Trainable params
> 0         Non-trainable params
> 0         Total params
> 0.000     Total estimated model params size (MB)
> /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/saforem2/genslm/venvs/polaris/2023-01-10/lib/python3.8/site-packages/pytorch_lightning/trainer/connectors/data_connector.py:240: PossibleUserWarning: The dataloader, train_dataloader, does not have many workers which may be a bottleneck. Consider increasing the value of the `num_workers` argument` (try 64 which is the number of cpus on this machine) in the `DataLoader` init to improve performance.
>   rank_zero_warn(
> Epoch 0:   0%|                                                                                                                                                                                                        | 0/32 [00:00<?, ?it/s]/soft/datascience/conda/2023-01-10/mconda3/lib/python3.8/site-packages/torch/distributed/distributed_c10d.py:2387: UserWarning: torch.distributed._all_gather_base is a private function and will be deprecated. Please use torch.distributed.all_gather_into_tensor instead.
>   warnings.warn(
> /soft/datascience/conda/2023-01-10/mconda3/lib/python3.8/site-packages/torch/distributed/distributed_c10d.py:2849: UserWarning: torch.distributed._reduce_scatter_base is a private function and will be deprecated. Please use torch.distributed.reduce_scatter_tensor instead.
>   warnings.warn(
> Epoch 0:   3%|████▉                                                                                                                                                          | 1/32 [00:00<00:28,  1.11it/s, loss=4.3, train/loss_step=4.300]STAGE:2023-01-25 21:58:20 13813:13813 ActivityProfilerController.cpp:294] Completed Stage: Warm Up
> Epoch 0:  12%|███████████████████▊                                                                                                                                          | 4/32 [00:02<00:16,  1.72it/s, loss=4.28, train/loss_step=4.150]STAGE:2023-01-25 21:58:21 13813:13813 ActivityProfilerController.cpp:300] Completed Stage: Collection
> [W collection.cpp:436] Warning: [pl][profile][LightningModule]DNATransformer.optimizer_step (function operator())
> STAGE:2023-01-25 21:58:23 13813:13813 output_json.cpp:417] Completed Stage: Post Processing
> Epoch 5: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 32/32 [00:12<00:00,  2.47it/s, loss=3.55, train/loss_step=3.460, train/loss_epoch=3.550]
> AVERAGE THROUGHPUT: 2.479620933532715 +- nan  samples/second over 1 ranks
> AVERAGE SECONDS PER SAMPLE: 0.40328747034072876 +- nan seconds/sample over 1 ranks
> Epoch 5: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 32/32 [00:12<00:00,  2.47it/s, loss=3.55, train/loss_step=3.460, train/loss_epoch=3.550]
> FIT Profiler Report
> Profile stats for: records
> -------------------------------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------
>                                                    Name    Self CPU %      Self CPU   CPU total %     CPU total  CPU time avg     Self CUDA   Self CUDA %    CUDA total  CUDA time avg    # of Calls
> -------------------------------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------
>                                           ProfilerStep*        12.72%     356.623ms        50.32%        1.411s     470.359ms       0.000us         0.00%     190.001ms      63.334ms             3
>                         [pl][profile]run_training_batch         0.07%       2.022ms        36.07%        1.012s     337.207ms       0.000us         0.00%     310.563ms     103.521ms             3
> [pl][profile][LightningModule]DNATransformer.optimiz...        18.56%     520.449ms        36.00%        1.010s     336.508ms       0.000us         0.00%     310.563ms     103.521ms             3
>       [pl][profile][Strategy]DeepSpeedStrategy.backward        20.93%     587.011ms        24.73%     693.371ms     231.124ms       0.000us         0.00%      34.362ms      11.454ms             3
> [pl][profile][Strategy]DeepSpeedStrategy.training_st...         2.98%      83.705ms        17.44%     488.994ms     162.998ms       0.000us         0.00%     465.664ms     155.221ms             3
>                                   cudaStreamSynchronize        13.54%     379.609ms        13.54%     379.609ms     454.622us       0.000us         0.00%       0.000us       0.000us           835
> autograd::engine::evaluate_function: EmbeddingBackwa...         0.00%      20.000us        13.23%     371.025ms     123.675ms       0.000us         0.00%     512.000us     170.667us             3
>                                      EmbeddingBackward0         0.00%      13.000us        13.23%     371.005ms     123.668ms       0.000us         0.00%     512.000us     170.667us             3
>                                aten::embedding_backward         0.00%       4.000us        13.23%     370.992ms     123.664ms       0.000us         0.00%     512.000us     170.667us             3
>                          aten::embedding_dense_backward         0.01%     300.000us        13.23%     370.988ms     123.663ms     492.000us         0.05%     512.000us     170.667us             3
>                                      record_param_comms         0.02%     514.000us        12.68%     355.520ms       9.876ms       0.000us         0.00%       0.000us       0.000us            36
>                                   cudaDeviceSynchronize        12.66%     354.915ms        12.66%     354.915ms      32.265ms       0.000us         0.00%       0.000us       0.000us            11
> enumerate(DataLoader)#_SingleProcessDataLoaderIter._...         5.33%     149.598ms         5.35%     149.889ms      49.963ms       0.000us         0.00%       0.000us       0.000us             3
>                                             aten::copy_         1.17%      32.870ms         4.20%     117.686ms      42.364us      46.316ms         4.47%      56.306ms      20.269us          2778
> autograd::engine::evaluate_function: torch::autograd...         1.12%      31.401ms         1.43%      40.212ms     134.040us       0.000us         0.00%       2.095ms       6.983us           300
> autograd::engine::evaluate_function: PreBackwardFunc...         0.07%       1.934ms         1.43%      40.156ms      93.604us       0.000us         0.00%      10.000us       0.023us           429
> autograd::engine::evaluate_function: PostBackwardFun...         0.06%       1.801ms         1.39%      38.930ms      94.034us       0.000us         0.00%     958.000us       2.314us           414
>                             PreBackwardFunctionBackward         1.35%      37.871ms         1.36%      38.222ms      89.096us       0.000us         0.00%      10.000us       0.023us           429
>                            PostBackwardFunctionBackward         1.27%      35.529ms         1.28%      35.974ms      86.894us       0.000us         0.00%       0.000us       0.000us           414
>                                         cudaMemcpyAsync         1.28%      35.825ms         1.28%      35.825ms      17.459us       3.612ms         0.35%       3.612ms       1.760us          2052
> -------------------------------------------------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------  ------------
> Self CPU time total: 2.804s
> Self CUDA time total: 1.037s
> 
> 130.76s user 16.33s system 104% cpu 2:20.40s total
> ```

