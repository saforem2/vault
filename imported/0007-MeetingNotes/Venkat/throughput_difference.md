

# 2023-10-10

- `MODEL_SIZE: GPT1T_2L, machine: Perlmutter, world_size: 32, env.SP_TYPE: megatron, args.micro_batch_size: 4, args.seq_length: 2048, args.global_batch_size: 128, args.zero_stage: 1, args.tensor_model_parallel_size: 8, args.pipeline_model_parallel_size: 1, args.data_parallel_size: 4`
    - Reported from Megatron-DeepSpeed:  `145` TFLOPS
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

- `MODEL_SIZE: GPT1T_2L, machine: Perlmutter, world_size: 32, env.SP_TYPE: megatron, args.micro_batch_size: 4, args.seq_length: 2048, args.global_batch_size: 128, args.zero_stage: 1, args.tensor_model_parallel_size: 8, args.pipeline_model_parallel_size: 1, args.data_parallel_size: 4`

    - Reported from Megatron-DeepSpeed:  `129` TFLOPS

    ```bash
    -------------------------- DeepSpeed Flops Profiler --------------------------
    Profile Summary at step 2:
    Notations:
    data parallel size (dp_size), model parallel size(mp_size),
    number of parameters (params), number of multiply-accumulate operations(MACs),
    number of floating-point operations (flops), floating-point operations per second (FLOPS),
    fwd latency (forward propagation latency), bwd latency (backward propagation latency),
    step (weights update latency), iter latency (sum of fwd, bwd and step latency)
    world size:                                                             32
    data parallel size:                                                     4
    model parallel size:                                                    8
    batch size per GPU:                                                     4
    params per GPU:                                                         2.14 B
    params of model = params per GPU * mp_size:                             17.1 B
    fwd MACs per GPU:                                                       17.66 TMACs
    fwd flops per GPU:                                                      35.33 T
    fwd flops of model = fwd flops per GPU * mp_size:                       282.61 T
    fwd latency:                                                            1.54 s
    fwd FLOPS per GPU = fwd flops per GPU / fwd latency:                    23 TFLOPS
    bwd latency:                                                            5.35 s
    bwd FLOPS per GPU = 2 * fwd flops per GPU / bwd latency:                13.21 TFLOPS
    fwd+bwd FLOPS per GPU = 3 * fwd flops per GPU / (fwd+bwd latency):      15.39 TFLOPS
    step latency:                                                           1.78 s
    iter latency:                                                           8.66 s
    FLOPS per GPU = 3 * fwd flops per GPU / iter latency:                   12.23 TFLOPS
    samples/second:                                                         14.77
    ----------------------------- Aggregated Profile per GPU -----------------------------


    ```
`
