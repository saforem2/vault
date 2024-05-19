# Megatron DeepSpeed (Intel)

## Llama2-7B


```bash
$ source savejobenv
# ssh $(qstat -x -f $(qstat -u $USER | tail -1 | sed "s/\..*$//g") | grep exec_host | sed "s/exec_host\ =\ //g" | sed "s/\/0\*64.*$//g" | sed "s/\/.$//g" | cut --delimiter="/" --fields=1)
$ eval "$(${HOME}/miniconda3/bin/conda shell.${SHELL} hook)" && conda activate anl_release_q4v2
$ source setenv.sh
$ cd "${HOME}/anl_24_release_q4/Megatron-DeepSpeed"
$ cd "${HOME}/anl_24_release_q4/llm.devkit/intel-extension-for-deepspeed/examples"
$ module unload oneapi/eng-compiler/2022.12.30.003 && module unload intel_compute_runtime/release/agama-devel-551 && module use -a /soft/modulefiles && module load oneapi/release/2023.12.15.001 && module use /home/ftartagl/graphics-compute-runtime/modulefiles && module load graphics-compute-runtime/agama-ci-devel-736.9
```


### Hostfile setup

```bash
cat $PBS_NODEFILE > hostfile
sed -e 's/$/ slots=12/' -i hostfile
echo "PATH=${PATH}" >> .deepspeed_env
echo "LD_LIBRARY_PATH=${LD_LIBRARY_PATH}" >> .deepspeed_env
echo "http_proxy=${http_proxy}" >> .deepspeed_env
echo "https_proxy=${https_proxy}" >> .deepspeed_env

sav

saveDeepSpeedenv() {
  EXAMPLES_DIR="${HOME}/anl_24_release_q4/llm.devkit/intel-extension-for-deepspeed/examples"
  HOSTFILE_MPICH="${EXAMPLES_DIR}/hostfile_mpich"
  HOSTFILE_DEEPSPEED="${EXAMPLES_DIR}/hostfile_deepspeed"
  cat "${HOSTFILE:-${PBS_NODEFILE}}" > "${HOSTFILE_MPICH}"
  sed -e 's/$/ slots=12/' -i "${HOSTFILE_MPICH}"
  echo "PATH=${PATH}" >> .deepspeed_env
  echo "LD_LIBRARY_PATH=${LD_LIBRARY_PATH}" >> .deepspeed_env
  echo "http_proxy=${http_proxy}" >> .deepspeed_env
  echo "https_proxy=${https_proxy}" >> .deepspeed_env
}
```



## 2024-01-24

- [x] Resolved `torch-ccl` install issues in `~/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/torch-ccl`
- [ ] 

```bash
# activate conda && load modules
$ eval "$(/home/foremans/miniconda3/bin/conda shell.zsh hook)" && conda activate anl_release_q4v2
$ module unload oneapi/eng-compiler/2022.12.30.003 \
    && module unload intel_compute_runtime/release/agama-devel-551 \
    && module use -a /soft/modulefiles \
    && module load oneapi/release/2023.12.15.001 \
    && module use /home/ftartagl/graphics-compute-runtime/modulefiles
    # && module load graphics-compute-runtime/agama-ci-devel-736.9
```
```bash
$ ds_report
/home/foremans/miniconda3/envs/anl_release_q4v2/bin/ds_report:4: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  __import__('pkg_resources').require('deepspeed==0.12.3+6ea44d02')
/home/foremans/miniconda3/envs/anl_release_q4v2/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ig
nore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
  warn(
[2024-01-24 07:36:33,277] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
[2024-01-24 07:36:43,867] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
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
 [WARNING]  async_io requires the dev libaio .so object and headers but these were not found.
 [WARNING]  async_io: please install the libaio-devel package with yum
 [WARNING]  If libaio is already installed (perhaps from source), try setting the CFLAGS and LDFLAGS environment variables to where it can be found.
async_io ............... [NO] ....... [NO]
cpu_adagrad ............ [NO] ....... [OKAY]
cpu_adam ............... [NO] ....... [OKAY]
flash_attn ............. [NO] ....... [OKAY]
fused_adam ............. [NO] ....... [OKAY]
quantizer .............. [NO] ....... [OKAY]
transformer ............ [NO] ....... [OKAY]
transformer_inference .. [NO] ....... [OKAY]
utils .................. [NO] ....... [OKAY]
--------------------------------------------------
DeepSpeed general environment info:
torch install path ............... ['/home/foremans/miniconda3/envs/anl_release_q4v2/lib/python3.9/site-packages/torch']
torch version .................... 2.1.0a0+cxx11.abi
deepspeed install path ........... ['/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/DeepSpeed/deepspeed']
deepspeed info ................... 0.12.3+6ea44d02, 6ea44d02, HEAD
deepspeed wheel compiled w. ...... torch 2.1 
shared memory (/dev/shm) size .... 503.61 GB
5.94s user 7.86s system 37% cpu 36.808s total
```


## Old

## Previous Install Issues
```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
$ bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
$ eval "$(/home/foremans/miniconda3/bin/conda shell.zsh hook)"

$ export DRM_LIB="$(pwd)/usr/include/libdrm"
$ conda config --add channels conda-forge && conda install -c conda-forge mpi4py -y --no-deps && conda install -c conda-forge libssh -y && conda uninstall mpi -y && python3 -m pip install -r requirements.txt && python3 -m pip install *.whl

1697  2024-01-22 16:29  module unload oneapi/eng-compiler/2022.12.30.003
 1698  2024-01-22 16:29  module unload intel_compute_runtime/release/agama-devel-551
 1699  2024-01-22 16:29  module use -a /soft/modulefiles
 1700  2024-01-22 16:29  module load oneapi/release/2023.12.15.001
 1701  2024-01-22 16:29  module use /home/ftartagl/graphics-compute-runtime/modulefiles
 1702  2024-01-22 16:29  module load graphics-compute-runtime/agama-ci-devel-736.9
 1703  2024-01-22 16:29  cd torch-ccl
 1704  2024-01-22 16:29  ls
 1705  2024-01-22 16:30  COMPUTE_BACKEND=dpcpp python3 setup.py develop |& tee build.log
 1706  2024-01-22 16:45  cd ../
 1707  2024-01-22 16:45  cd intel-extension-for-deepspeed
 1708  2024-01-22 16:45  python3 setup.py develop |& tee build.log
 1709  2024-01-22 16:48  ../
 1710  2024-01-22 16:48  cd DeepSpeed
 1711  2024-01-22 16:48  ls
 1712  2024-01-22 16:48  python3 -m pip install -r requirements/requirements.txt
 python3 setup.py develop |& tee build.log
```

`module unload oneapi/eng-compiler/2022.12.30.003 && module unload intel_compute_runtime/release/agama-devel-551&& module use -a /soft/modulefiles && module load oneapi/release/2023.12.15.001 && module use /home/ftartagl/graphics-compute-runtime/modulefiles && module load graphics-compute-runtime/agama-ci-devel-736.9`


## Using `ezpz` `launch`

- Take 1:

    ```bash
      
      $ launch python3 pretrain_llama.py \
      		--tensor-model-parallel-size 1 \
      		--pipeline-model-parallel-size 1
            --num-layers 32 \ \
            --hidden-size 4096\ \
            --ffn-hidden-size 5504\ \
            --num-attention-heads 32\ \
            --micro-batch-size 1\ \
            --global-batch-size 24\ \
            --seq-length 2048\ \
            --max-position-embeddings 2048\ \
            --train-iters 250000\ \
            --save /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/checkpoints/LLAMA_7B_LLAMA_7B_z3_seqlen_mp1_pp1_sp24_nl32_hs4096_gb24_mb1\ \
            --load /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/checkpoints/LLAMA_7B_LLAMA_7B_z3_seqlen_mp1_pp1_sp24_nl32_hs4096_gb24_mb1\ \
            --data-path \ \
            --data-impl mmap\ \
            --tokenizer-type GPTSentencePieceTokenizer\ \
            --tokenizer-model ./tmp/tokenizer.model\ \
            --split 949,50,1\ \
            --distributed-backend ccl\ \
            --lr 3e-4\ \
            --lr-decay-style cosine\ \
            --min-lr 3e-5\ \
            --weight-decay 0.1\ \
            --clip-grad 1\ \
            --lr-warmup-iters 2000\ \
            --optimizer adam\ \
            --adam-beta1 0.9\ \
            --adam-beta2 0.95\ \
            --log-interval 1\ \
            --save-interval 10000\ \
            --eval-interval 1000\ \
            --eval-iters 10\ \
            --bf16\ \
            --no-query-key-layer-scaling\ \
            --attention-dropout 0\ \
            --hidden-dropout 0\ \
            --use-rotary-position-embeddings\ \
            --untie-embeddings-and-output-weightss\ \
            --swiglus\ \
            --normalization rmsnorms\ \
            --disable-bias-linears\ \
            --num-key-value-heads 4s\ \
            --tensorboard-dir /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/outputs/LLAMA_7B_LLAMA_7B_z3_seqlen_mp1_pp1_sp24_nl32_\ \
            hs4096_gb24_mb1/tensorboards\ \
            --log-timers-to-tensorboards\ \
            --tensorboard-log-interval 1s\ \
            --data-path /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/dataset/BookCorpusDataset_text_documents\ \
            --vocab-file /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/dataset/gpt2-vocab.jsons\ \
            --merge-file /lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/data\ \
            set/gpt2-merges.txt s\ \
            --zero-stage=3 s\ \
            --deepspeed_config=/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/deepspeed.json s\ \
            --deepspeed\ \
        Connected to tcp://x4502c1s0b0n0.hostmgmt2502.cm.aurora.alcf.anl.gov:7919
        Found executable /home/foremans/miniconda3/envs/anl_release_q4/bin/python3
        Launching application 2e559157-da5e-4185-9902-dc8d932e8bb3
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        /home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torchvision/io/image.py:13: UserWarning: Failed to load image Python extension: ''If you don't plan on using image functionality from `torchvision.io`, you can ignore this warning. Otherwise, there might be something wrong with your environment. Did you have `libjpeg` or `libpng` installed before building `torchvision` from source?
          warn(
        [2024-01-23 00:02:13,326] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,327] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,327] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,327] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,329] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,329] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,331] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,332] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,332] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,333] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,333] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:13,399] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,144] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,145] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,146] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,147] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,151] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,151] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,152] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,153] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,154] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,154] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,155] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:14,207] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
        [2024-01-23 00:02:19,177] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,177] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,177] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,179] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,179] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,179] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,180] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,180] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,180] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,180] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,180] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,180] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,183] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,183] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,183] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,207] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,207] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,207] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,304] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,304] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,305] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,311] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,311] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,311] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,313] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,313] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,313] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,313] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,314] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,314] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,314] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,314] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,314] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,315] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,315] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,315] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,316] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,316] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,316] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,316] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,316] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,316] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,317] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,317] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,317] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,317] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,317] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,317] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,318] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,318] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,318] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,352] [INFO] [comm.py:161:init_deepspeed_backend] Initialize ccl backend
        [2024-01-23 00:02:19,352] [INFO] [comm.py:637:init_distributed] cdb=None
        [2024-01-23 00:02:19,352] [INFO] [comm.py:652:init_distributed] Not using the DeepSpeed or dist launchers, attempting to detect MPI environment...
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=3, local_rank=3, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=9, local_rank=9, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=11, local_rank=11, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=1, local_rank=1, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=2, local_rank=2, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=4, local_rank=4, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=5, local_rank=5, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=6, local_rank=6, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=7, local_rank=7, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=13, local_rank=1, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=8, local_rank=8, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=10, local_rank=10, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=0, local_rank=0, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,889] [INFO] [comm.py:668:init_distributed] Initializing TorchBackend in DeepSpeed with backend ccl
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=15, local_rank=3, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=17, local_rank=5, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=19, local_rank=7, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=21, local_rank=9, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=12, local_rank=0, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=14, local_rank=2, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=16, local_rank=4, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=18, local_rank=6, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=20, local_rank=8, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=22, local_rank=10, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:19,888] [INFO] [comm.py:702:mpi_discovery] Discovered MPI settings of world_rank=23, local_rank=11, world_size=24, master_addr=10.115.53.137, master_port=29500
        [2024-01-23 00:02:20][INFO][dist:257] - DistInfo={
            "DEVICE": "xpu",
            "DEVICE_ID": "xpu:0",
            "DISTRIBUTED_BACKEND": "gloo",
            "GPUS_PER_NODE": 12,
            "HOSTFILE": "/var/spool/pbs/aux/604213.aurora-pbs-0001.hostmgmt.cm.aurora.alcf.anl.gov",
            "HOSTNAME": "x4502c1s0b0n0.hostmgmt2502.cm.aurora.alcf.anl.gov",
            "HOSTS": "['x4502c1s0b0n0', 'x4502c1s3b0n0']",
            "LOCAL_RANK": 0,
            "MACHINE": "Aurora",
            "NGPUS": 24,
            "NODE_ID": 0,
            "NUM_NODES": 2,
            "RANK": 0,
            "SCHEDULER": "PBS",
            "WORLD_SIZE_IN_USE": 24,
            "WORLD_SIZE_TOTAL": 24
        }
        [2024-01-23 00:02:20,987] [INFO] [real_accelerator.py:158:get_accelerator] Setting ds_accelerator to xpu (auto detect)
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
        
        [2024-01-23 00:02:20][INFO][spawn:38] - icx -Wno-unused-result -Wsign-compare -DNDEBUG -fwrapv -O2 -Wall -fPIC -O2 -isystem /home/foremans/miniconda3/envs/anl_release_q4/include -fPIC -O2 -isystem /home/foremans/miniconda3/envs/anl_release_q4/include -fPIC -c /tmp/tmph01efr3s/test.c -o /tmp/tmph01efr3s/test.o
        WARNING: TensorBoard writing requested but is not available (are you using PyTorch 1.1.0 or later?), no TensorBoard logs will be written.
        2024:01:23-00:02:21:(122507) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122510) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122515) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122516) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122508) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122509) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122511) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122512) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122513) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122514) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122517) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122518) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(122510) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122515) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122507) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122508) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122509) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122511) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122512) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122513) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122514) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122516) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122517) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(122518) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141071) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141072) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141073) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141075) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141076) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141078) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141079) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141081) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141074) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141077) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141080) |CCL_WARN| could not get local_idx/count from environment variables, trying to get them from ATL
        2024:01:23-00:02:21:(141071) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141075) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141078) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141081) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141072) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141073) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141074) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141076) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141077) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141079) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        2024:01:23-00:02:21:(141080) |CCL_ERROR| global.cpp:150 getenv_local_coord: condition global_data::env().ze_ipc_exchange == ccl::ze::ipc_exchange_mode::sockets failed
        to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        >fused kernel is only supported in cuda, skip loading fused kernel
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        Traceback (most recent call last):
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 583, in <module>
            model = main()
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/pretrain_llama.py", line 561, in main
            model = pretrain(
          File "/lus/gecko/projects/Aurora_deployment/foremans/anl_24_release_q4/llm.devkit/Megatron-DeepSpeed/megatron/training.py", line 136, in pretrain
            torch.distributed.all_reduce(start_time_tensor,
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/c10d_logger.py", line 47, in wrapper
            return func(*args, **kwargs)
          File "/home/foremans/miniconda3/envs/anl_release_q4/lib/python3.9/site-packages/torch/distributed/distributed_c10d.py", line 2050, in all_reduce
            work = group.allreduce([tensor], opts)
        RuntimeError: oneCCL: global.cpp:150 getenv_local_coord: EXCEPTION: to get local_idx/count from ATL, set CCL_ZE_IPC_EXCHANGE=sockets explicitly
        ```
