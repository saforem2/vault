# `flash-attn` on Sunspot

## 🐛 `flash-attn` bug / Loss Discrepancy

In the `q4-drop`, it was observed that toggling `flash-attn` on / off seemed to produce different loss curves (with otherwise *identical configs*)

```yaml title="aGPT-2B-common.yml"
TP: 1
PP: 1
GAS: 1
OPT: adamw
dtype: bf16
NLAYERS: 10
MICRO_BATCH: 2
WORLD_SIZE: 24
```

This can be seen clearly in the figure below:

![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-bug-q4-drop-sunspot-1.png)

This was identified, and to be addressed in upcoming release.

## LLM Framework Release 

### \[05/14/2024\]: Initial Release

On 05/14/2024, Intel dropped their new LLM frameworks release:

> [!summary]- `frameworks_2024_5_v2` Announcement
>
> Hi Venkat,
> 
> We have shared the official Q2 release in two different forms :
> 
> Manual Setup: `/gila/Aurora_deployment/anl_24_q2_release.tar.gz`
> 
> and 
> 
> Module: 
> 
> `module use -a /home/jmitche1/anl_release/2024/q2`
> 
> `module load frameworks_2024_5_v2`
> 
>  Instructions on how to use modules with Q2 build are anl_24_q2_release/README
> 
> - **The release includes :**
> 	- Megatron-DeepSpeed 0.14.2 (with patch)
> 	- Intel® Extension for PyTorch* v2.1.30+xpu
> 	- TorchCCL 2.1.300
> 	- ONEAPI 2024.1.0.596.PUBLIC_IDP_2024.1.0_723
> 	- Agama driver: 803.29
> 
> - The release provides following key features:
> 	- Scaleup Performance improvement from the `TorchCCl` prototype feature enabled by `TORCH_LLM_ALLREDUCE=1`  [details](https://urldefense.us/v3/__https://github.com/intel/torch-ccl/releases/tag/v2.1.300*2Bxpu__;JQ!!G_uCfscf7eWS!ZDMnN0Oxp1sCv06MkdlBqFIq0NMAXaCBOtl3fEtBq8Fn4-3iYY5-kPEKr-q4vZIL_i6f2wQbULxAIFJAthJyu3VvNA$)
> 	- Auto TP inference support for more workloads
> 	- Flash Attention V2 improvement for 256 head dimension support; MiCS support.
> 	- Latest Features and Optimizations from DeepSpeed [0.14.2](https://urldefense.us/v3/__https://github.com/microsoft/DeepSpeed/releases/tag/v0.14.2__;!!G_uCfscf7eWS!ZDMnN0Oxp1sCv06MkdlBqFIq0NMAXaCBOtl3fEtBq8Fn4-3iYY5-kPEKr-q4vZIL_i6f2wQbULxAIFJAthLj8rV_rA$) and Intel® Extension for PyTorch* [2.1.30](https://urldefense.us/v3/__https://github.com/intel/intel-extension-for-pytorch/tree/v2.1.30*2Bxpu__;JQ!!G_uCfscf7eWS!ZDMnN0Oxp1sCv06MkdlBqFIq0NMAXaCBOtl3fEtBq8Fn4-3iYY5-kPEKr-q4vZIL_i6f2wQbULxAIFJAthL8hknZQg$).
> 
> Thanks,   
> Jerome

With this new release, Intel observed that the loss curves agreed exactly for `flash` / no-`flash`, using the learning rate settings below:

```yaml title="lr00015-decay320k-warmup01.yaml"
lr: 0.00015
lr_warmup_frac: 0.01
lr_decay_iters: 320000
```

Testing with Jerome's new release:

```bash title="anl_24_q2_release.sh"
module use -a /home/jmitche1/anl_release/2024/q2 ; module load frameworks_2024_5_v2
```

I was able to independently confirm these results, shown in [[#flash 🤝 no-flash]]

### flash 🤝 no-flash

> [!NOTE]- `wandb` runs
> 
> <details open><summary><code>wandb</code> runs:</summary>
> 
> - \[✅ `flash`\] W&B Run: [youthful-river-1832](https://wandb.ai/aurora_gpt/AuroraGPT/runs/716r5rnq/overview?nw=nwuserforemans)
> - \[❌ `flash`\] W&B Run: [earthy-wave-1830](https://wandb.ai/aurora_gpt/AuroraGPT/runs/120ln0b4/overview?nw=nwuserforemans)
> 
> </details>
 
![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-true-2024-1.png) ![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-false-2024-1.png)

### Broken MPI ??

For whatever reason, coming back the next day (05/15/2024) and trying to
continue running experiments I was met with a new MPI crash on initialization.

See the following slack threads for additional details and related discussion:

- [thread 1](https://cels-anl.slack.com/archives/C05V0SRAVB6/p1715867557424879)

I was able to resolve this issue by creating a new `conda` environment and re-installing `mpi4py`.


In an effort to attempt to understand the cause of this behavior, it was
identified that the loss curves seem to agree when using a different `{LR,
LR_WARMUP_FRAC, LR_DECAY_ITERS}`:

### 🥸 Fix in Disguise

- [ ] Repeat the experiments below using the `2024.0` frameworks to make sure they _all_ agree
- [ ] 

![[flash-attn-disguise-decay10000.png]]


![[disguised-fix-1.png]] ![[disguised-fix-2.png]]

### `2024.0` Fix

**Everything** seems to work with

```bash
module load frameworks/2023.12.15.001
```

![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-2024-0-fix.png) ![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/flash-attn-fix-frameworks-comparison.png)


## `lr-decay-iters` dependence

![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/lr-schedule-dependence.png)

![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/lr-decay-iters-dependence-1.png) ![](0001-Work/Aurora-GPT/0001-AuroraGPT/assets/lr-decay-iters-dependence-2.png

