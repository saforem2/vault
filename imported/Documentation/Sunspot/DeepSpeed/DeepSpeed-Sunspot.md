# DeepSpeed Installation instructions on Sunspot:

- Support accelerator abstraction in DeepSpeed – [microsoft/DeepSpeed/pull/2471](https://github.com/microsoft/DeepSpeed/pull/2471):
    - Adds support for Intel GPU via `get_accelerator()` abstraction

This document describes install instructions for DeepSpeed on Sunspot.

Currently, we support multicards training of [GPT2](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) on single node and 6 PVC cards.

The codebase is capable of training a 30-layer, 3.6 Billion Parameter GPT2 Language Model across Intel GPUs. 

## System Login 

```Shell
$ ssh username@auroravendor.alcf.anl.gov  
$ ssh sunspot-uan01.sunspot.alcf.anl.gov 
$ # Allocate a node on Sunspot 
$ qsub -I -q workq -l select=1,walltime=120:00 -A Aurora_deployment 
```

## Setup

```Shell
$ source /soft/restricted/CNDA/frameworks/Megatron-LM/helper_exports.sh 
```

We officially support `python3.9.7` and strongly recommend to install an Anaconda environment 

- If Anaconda is not installed on system:

```Shell
$ wget https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh
$ bash Anaconda3-2018.12-Linux-x86_64.sh
$ conda create --name llm python=3.9.7
$ conda activate llm 
```
 
### Install Dependencies via wheel `*.whl` files

```Shell
$ pip install "/soft/restricted/CNDA/frameworks/2022.11.15.001/wheels/pytorch/torch-1.10.0a0+git90332b4-cp39-cp39-linux_x86_64.whl"
$ pip install "/soft/restricted/CNDA/frameworks/2022.11.15.001/wheels/pytorch/intel_extension_for_pytorch-1.10.200+gpu-cp39-cp39-linux_x86_64.whl"
$ declare -x IPEX_TILE_AS_DEVICE="1" 
$ pip install "/soft/restricted/CNDA/frameworks/2022.11.15.001/wheels/pytorch/oneccl_bind_pt-1.10.200+gpu-cp39-cp39-linux_x86_64.whl"
```

### Install DeepSpeed and Intel® Extension for DeepSpeed* via Compiling from Source

#### Clone Source Code of DeepSpeed

```Shell
$ conda install -y git cmake ninja 
$ mkdir $HOME/anl_release 
$ cd $HOME/anl_release 
$ git clone https://github.com/microsoft/DeepSpeed frameworks.ai.benchmarking.other.deepspeed 
$ git fetch origin pull/2471/head:xpu_support 
$ git checkout xpu_support 
$ git submodule sync --recursive 
$ git submodule update --init --recursive 
```

### Clone Source Code of Intel Extension for DeepSpeed

```Shell
$ cd $HOME/anl_release 
$ git clone https://github.com/intel/intel-extension-for-deepspeed 
```
 
### Install Intel® Extension for DeepSpeed and DeepSpeed:

```Shell
$ cd intel-extension-for-deepspeed 
$ pip install -r examples/Megatron-LM/requirements.txt 
$ python setup.py develop
$ cd $HOME/anl_release
$ cd frameworks.ai.benchmarking.other.deepspeed
$ pip install -r requirements/requirements.txt
$ CC=dpcpp CFLAGS=-fPIC CXX=dpcpp CXXFLAGS=-fPIC DS_BUILD_DEVICE=dpcpp DS_BUILD_CPU_ADAM=1 DS_BUILD_FUSED_ADAM=1 DS_BUILD_QUANTIZER=1 DS_BUILD_STOCHASTIC_TRANSFORMER=1  DS_BUILD_TRANSFORMER=1 DS_BUILD_UTILS=1 python setup.py develop
```

#### Update: 2023-02-01

```Shell
$ cd intel-extension-for-deepspeed 
$ pip install -r examples/Megatron-LM/requirements.txt 
$ python setup.py develop
$ cd $HOME/anl_release
$ cd frameworks.ai.benchmarking.other.deepspeed
$ pip install -r requirements/requirements.txt
$ CC=dpcpp CFLAGS=-fPIC CXX=dpcpp CXXFLAGS=-fPIC DS_BUILD_DEVICE=dpcpp DS_BUILD_CPU_ADAM=1 DS_BUILD_FUSED_ADAM=1 DS_BUILD_QUANTIZER=1 DS_BUILD_STOCHASTIC_TRANSFORMER=1  DS_BUILD_TRANSFORMER=1 DS_BUILD_UTILS=1 python setup.py develop
```

### Retrieve WebText Data

```Shell
$ cp  -r \
    /soft/restricted/CNDA/frameworks/Megatron-LM/frameworks.ai.benchmarking.other.deepspeedexamples/Megatron-LM/data* \
    $HOME/anl_release/intel-extension-for-deepspeed/examples/Megatron-LM 
$ cp  -r \
    /soft/restricted/CNDA/frameworks/Megatron-LM/frameworks.ai.benchmarking.other.deepspeedexamples/Megatron-LM/gpt2_local  \
    $HOME/anl_release/intel-extension-for-deepspeed/examples/Megatron-LM  
```

### Examples using Megatron-LM

Set the data source to support webtext by modifying the option `--train-data` from `c4/en` to `webtext`:

```Shell
$ vi $HOME/anl_release/intel-extension-for-deepspeed/examples/Megatron-LM/scripts/gpt-3.6b.sh
    $ # --train-data from c4/en to webtext
$ # ------------------------------------
$ cd $HOME/anl_release/intel-extension-for-deepspeed/examples/Megatron-LM
$ ./scripts/gpt-3.6b.sh 
```

```Shell
$ cat $HOME/anl_release/intel-extension-for-deepspeed/examples/Megatron-LM/scripts/gpt-3.6b.sh
#! /bin/bash

# Change for multinode config
MP_SIZE=2

NUM_WORKERS=2
NUM_GPUS_PER_WORKER=12


script_path=$(realpath $0)
script_dir=$(dirname $script_path)

config_json="$script_dir/ds_zero2_config_bf16.json"
gpt_options=" \
       --model-parallel-size ${MP_SIZE} \
       --num-layers 30 \
       --hidden-size 3072 \
       --num-attention-heads 32 \
       --batch-size 8 \
       --seq-length 2048 \
       --max-position-embeddings 2048 \
       --train-iters 10 \
       --resume-dataloader \
       --train-data webtext \
       --lazy-loader \
       --tokenizer-type GPT2BPETokenizer \
       --split 949,50,1 \
       --distributed-backend ccl \
       --lr 0.00015 \
       --no-load-optim \
       --lr-decay-style cosine \
       --weight-decay 1e-2 \
       --clip-grad 1.0 \
       --warmup .01 \
       --checkpoint-activations \
       --deepspeed-activation-checkpointing \
       --bf16 \
"
gpt_options="${gpt_options}
               --deepspeed \
               --deepspeed_config ${config_json} \
"

ds_args=""
gpt2_args=""

for i in "$@"; do
  if [[ $i =~ "--oneprof_args" ]]; then
    ds_args="$ds_args $i"
  elif [[ $i =~ "--onetrace_args" ]]; then
    ds_args="$ds_args $i"
  else
    gpt2_args="$gpt2_args $i"
  fi
done

run_cmd="deepspeed $ds_args --hostfile hostfile --num_nodes ${NUM_WORKERS} --num_gpus ${NUM_GPUS_PER_WORKER} pretrain_gpt2.py ${gpt_options} $gpt2_args"
echo ${run_cmd}
eval ${run_cmd}

set +x
```