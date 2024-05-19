
# Megatron-DeepSpeed

- [microsoft/Megatron-DeepSpeed](https://github.com/microsoft/Megatron-DeepSpeed)
- `/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/microsoft/Megatron-DeepSpeed/pretrain_gpt.sh`

## 2023-02-14

> [!success] Single GPU on ThetaGPU
> - [x] Working on single GPU of ThetaGPU

> [!success] Multi Node on ThetaGPU
> - [x] Working on multi-GPU of ThetaGPU:
>     - `/lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/microsoft/Megatron-DeepSpeed/pretrain_gpt-multinode-2023-02-14-3.log`

> [!note]- # Pretrain GPT
> ```bash
> $ cat ~/datascience/foremans/locations/thetaGPU/projects/microsoft/Megatron-DeepSpeed/pretrain_gpt.sh
> #!/bin/bash --login
> 
> TSTAMP=$(date "+%Y-%m-%d-%H%M%S")
> 
> # Change for multinode config
> HOSTFILE=$COBALT_NODEFILE
> NRANKS=$(wc -l < ${HOSTFILE})
> NGPU_PER_RANK=$(nvidia-smi -L | wc -l)
> NGPUS=$((${NRANKS}*${NGPU_PER_RANK}))
> 
> NODE_RANK=0
> NNODES=$NRANKS
> GPUS_PER_NODE=$NGPU_PER_RANK
> WORLD_SIZE=$NGPUS
> 
> module load conda/2022-07-01
> conda activate base
> conda activate /lus/grand/projects/datascience/foremans/locations/thetaGPU/miniconda3/envs/2022-07-01
> source ./venvs/thetaGPU/2022-07-01-deepspeed/bin/activate
> 
> export WANDB_CACHE_DIR=".cache/wandb"
> export CFLAGS="-I${CONDA_PREFIX}/include/"
> export LDFLAGS="-L${CONDA_PREFIX}/lib/"
> 
> TP=8
> PP=16
> NLAYERS=24
> HIDDEN=1024
> GLOBAL_BATCH=64
> MICRO_BATCH=4
> ZERO_STAGE=1
> RUN_STR=ds_z${ZERO_STAGE}_nl${NLAYERS}_hs${HIDDEN}_gb${GLOBAL_BATCH}_mb${MICRO_BATCH}
> OUTPUT_DIR="./outputs/${RUN_STR}"
> mkdir -p $OUTPUT_DIR
> 
> CHECKPOINT_DIR="./checkpoints/$RUN_STR"
> TENSORBOARD_DIR="./outputs/${RUN_STR}/tensorboard"
> export TENSORBOARD_DIR=$TENSORBOARD_DIR
> export NCCL_DEBUG=warn
> 
> DATA_PATH="./dataset/BookCorpusDataset_text_document"
> 
> DS_CONFIG=./ds_config-gpt.json
> `cat <<EOT > $DS_CONFIG
> {
>   "train_batch_size" : $GLOBAL_BATCH,
>   "train_micro_batch_size_per_gpu": $MICRO_BATCH,
>   "steps_per_print": 1,
> 
>   "zero_optimization": {
>     "stage": $ZERO_STAGE
>   },
> 
>   "fp16": {
>     "enabled": true,
>     "initial_scale_power": 12
>   },
> 
>   "wall_clock_breakdown" : true,
> 
>   "flops_profiler": {
>     "enabled": true,
>     "profile_step": -1,
>     "module_depth": -1,
>     "top_modules": 1,
>     "detailed": true,
>     "output_file": null
>   },
> 
>   "wandb": {
>     "enabled": true,
>     "project": "megatron-LM"
>   }
> }
> EOT`
> ds_args=""
> ds_args=" --deepspeed ${ds_args}"
> ds_args=" --deepspeed_mpi ${ds_args}"
> # ds_args=" --no-pipeline-parallel ${ds_args}"
> ds_args=" --deepspeed_config=$DS_CONFIG ${ds_args}"
> ds_args=" --zero-stage=$ZERO_STAGE ${ds_args}"
> ds_args=" --deepspeed-activation-checkpointing ${ds_args}"
> 
> # --save $CHECKPOINT_DIR \
> # --load $CHECKPOINT_DIR \
> gpt_args="\
>   --tensor-model-parallel-size $TP \
>   --pipeline-model-parallel-size $PP \
>   --num-layers $NLAYERS \
>   --hidden-size $HIDDEN \
>   --num-attention-heads 16 \
>   --micro-batch-size 4 \
>   --global-batch-size 16 \
>   --seq-length 1024 \
>   --max-position-embeddings 1024 \
>   --train-iters 100 \
>   --lr-decay-iters 320000 \
>   --data-path $DATA_PATH \
>   --vocab-file gpt2-vocab.json \
>   --merge-file gpt2-merges.txt \
>   --data-impl mmap \
>   --split 949,50,1 \
>   --distributed-backend nccl \
>   --lr 0.00015 \
>   --lr-decay-style cosine \
>   --min-lr 1.0e-5 \
>   --weight-decay 1e-2 \
>   --clip-grad 1.0 \
>   --lr-warmup-fraction .01 \
>   --checkpoint-activations \
>   --log-interval 1 \
>   --save-interval 100 \
>   --eval-interval 50 \
>   --eval-iters 100 \
>   --tensorboard-dir . \
>   --log-timers-to-tensorboard \
>   --tensorboard-log-interval 5 \
>   --fp16"
> 
> MPI_COMMAND=$(which mpirun)
> MPI_FLAGS="--verbose \
>   -n $NGPUS \
>   -npernode ${NGPU_PER_RANK} \
>   --hostfile ${HOSTFILE} \
>   -x CFLAGS \
>   -x LDFLAGS \
>   -x PYTHONUSERBASE \
>   -x http_proxy \
>   -x https_proxy \
>   -x PATH \
>   -x LD_LIBRARY_PATH"
> 
> ${MPI_COMMAND} \
>   ${MPI_FLAGS} \
>   $(which python3) \
>   ./pretrain_gpt.py \
>   ${gpt_args} \
>   ${ds_args} \
>   --exit-interval 5000 | tee ${OUTPUT_DIR}/output.log
> ```

## 2023-02-13

> [!success] Single GPU on ThetaGPU
> - [x] Working on single GPU of ThetaGPU

> [!error] Multi Node on ThetaGPU
> - [ ] Gets hung trying to launch with `mpirun`
> - [ ] Related issue: [The process is stuck at this step:compiling and loading fused kernels ... #93](https://github.com/microsoft/Megatron-DeepSpeed/issues/93#top)
> ```Shell
> ...
> Emitting ninja build file /lus/grand/projects/datascience/foremans/locations/thetaGPU/projects/microsoft/Megatron-DeepSpeed/megatron/fused_kernels/build/build.ninja...
> Building extension module fused_mix_prec_layer_norm_cuda...
> Allowing ninja to set a default number of workers... (overridable by setting the environment variable MAX_JOBS=N)
> ninja: no work to do.
> Loading extension module fused_mix_prec_layer_norm_cuda...
> Loading extension module fused_mix_prec_layer_norm_cuda...
> Loading extension module fused_mix_prec_layer_norm_cuda...
> Loading extension module fused_mix_prec_layer_norm_cuda...
> >>> done with compiling and loading fused kernels. Compilation time: 332.899 seconds
> # (stuck here)
> ```

