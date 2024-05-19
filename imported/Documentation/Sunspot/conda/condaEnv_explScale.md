
# Explicit Scaling on Sunspot

Conda information + Environment variables

```bash
#!/bin/bash

module restore
module unload oneapi
module load frameworks/.2022.11.15.002
module load tools/pti-gpu/887839-2022.11.22 # sysmon

source $IDPROOT/bin/activate
conda activate $AURORA_MODELS_PT_BASE_ENV
#conda activate $AURORA_MODELS_PT_HVD_ENV
#conda activate $AURORA_MODELS_PT_DDP_ENV

export PATH=$PATH:/soft/tools/igt-gpu-tools/master-2022.05.26/bin/ # for intel_gpu_top
export ZE_AFFINITY_MASK=0.0,0.1,1.0,1.1,2.0,2.1,3.0,3.1,4.0,4.1,5.0,5.1
export EnableImplicitScaling=0
export IPEX_TILE_AS_DEVICE=1
export IPEX_XPU_ONEDNN_LAYOUT_OPT=1
export CCL_LOG_LEVEL=INFO
export CCL_ZE_QUEUE_INDEX_OFFSET=0
export CCL_SYCL_OUTPUT_EVENT=0
export CCL_OP_SYNC=1
export HOROVOD_LOG_LEVEL=INFO
export HOROVOD_CCL_FIN_THREADS=1
export HOROVOD_CCL_ADD_EXTRA_WAIT=1
export HOROVOD_FUSION_THRESHOLD=150000000
export HOROVOD_CYCLE_TIME=0.1


## Default on Sunspot
# EnableImplicitScaling=0
# ZE_AFFINITY_MASK= NOT SET
# CCL_WORKER_AFFINITY= NOT SET
# HOROVOD_THREAD_AFFINITY NOT SET
# ITEX_TILE_AS_DEVICE=1
# ITEX_LAYOUT_OPT=1
# IPEX_TILE_AS_DEVICE=1
# IPEX_XPU_ONEDNN_LAYOUT_OPT=1
```