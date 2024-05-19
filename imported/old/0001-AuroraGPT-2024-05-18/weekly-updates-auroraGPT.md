# 📆 Weekly Updates

## 2024-05

<details closed><summary><b>[</b><code>2024-05-03</code><b>]</b></summary>

1. Updates:
    - Working on testing new software stack (with `CUDA=12.2`) on Polaris
        - Building + testing base `conda/2024-04-29` environment
        - Verified and confirmed Dolma v1.7 with new software stack on Polaris
    - Attended RIKEN / Argonne AuroraGPT Collabotation
    - Working with Intel to identify / resolve flash attention issue on Sunspot
    - Working on mechanism for converting Megatron checkpoints to Huggingface compatible format
2. Blockers:
    - Software upgrade on Polaris
    - Queue depths on Sunspot

</details>


## 2024-04


<details closed><summary><b>[</b><code>2024-04-25</code><b>]</b></summary>

1. Updates:
    - distributed initial checkpoint **for testing functionality** of
      `aGPT-7B-P`.
        - details:
            - trained on 48 Nodes of Polaris
            - 4600 iterations
            - total of ~ 14 B tokens
    - Installed + tested new software stack on Sirius using `CUDA==12.2`
        - Removed hard `apex` dependency, will fallback to native `torch`
          implementations
    - added option to run in `DEBUG`  mode (i.e. `DEBUG=1 bash train_llama_alcf.sh`)
        - essentially just sets set -euxo pipefail [here](https://github.com/argonne-lcf/Megatron-DeepSpeed/blob/76816429d49a3160c15aa76efac223bda0d851f6/train_llama_alcf.sh#L8-L11) in `train_llama_alcf.sh#L8-L11`
    - Tested pre-training with full `dolma-v1.7` on Sunspot
        - added `dolma==1.7` data file lists to [`ALCF/data-lists/sunspot/*.txt`](https://github.com/argonne-lcf/Megatron-DeepSpeed/tree/main/ALCF/data-lists/sunspot)
        - added [`ALCF/sunspot-env.sh`](https://github.com/argonne-lcf/Megatron-DeepSpeed/blob/main/ALCF/sunspot-env.sh)
        - fixed `--use-flash-attn-builder` issue on Sunspot that was introduced from
          [recent change](https://github.com/microsoft/Megatron-DeepSpeed/commit/3c5f47563f697702c1e305fa01b7563f54b747fc)
          in microsoft/Megatron-DeepSpeed 
            - to disable `flash-attn` on Sunspot, run with:

              ```bash
              $ NO_FLASH_ATTN=1 bash train_llama_alcf.sh
              ```
    - added:
        - [ALCF/test_sunspot.sh](https://github.com/argonne-lcf/Megatron-DeepSpeed/blob/main/ALCF/test_sunspot.sh)
        - [ALCF/test_sirius.sh](https://github.com/argonne-lcf/Megatron-DeepSpeed/blob/main/ALCF/test_sirius.sh)
        - to run:
            - Launch interactive job (`qsub -I ...`)
            - Activate your `conda` environment
            - Navigate into `argonne-lcf/Megatron-DeepSpeed`, and launch:
              ```bash
              $ ALCF/test_sunspot.sh
              ```
        - **NOTE**: you may need to modify this `setup_conda()` function to
          properly use your personal conda environment

2. Blockers:
    - Polaris down for maintenance from 2024-04-22 to 2024-04-25
        - During downtime, worked on building + verifying software stack on
        Sirius to ensure everything works for Polaris' return

</details>

<details closed><summary><b>[</b><code>2024-04-19</code><b>]</b></summary>

1. Updates:
    - Working on gathering checkpoints to send to other teams for testing workflow / pipeline functionality
        - $\text{\textcolor{red}{NOTE}}$: **This is strictly to test for functionality**.
       	    - The models contained in the provided checkpoints should not be expected to output anything meaningful. 
    - Ongoing work to test methods for preventing "catastrophic loss" spikes during training
        - Catastrophic loss spikes seem to occur immediately at the end of the learning rate warmup and can cause the training run to crash with `NaN`
            - Ongoing work to confirm this is the case and to device strategy for alleviating
        - Added support for new optimizers:
            - [deepspeed.ops.FusedLamb](https://deepspeed.readthedocs.io/en/latest/_modules/deepspeed/ops/lamb/fused_lamb.html#FusedLamb)
            - [facebookresearch/schedule_free](https://github.com/facebookresearch/schedule_free)
                - [Fix checkpointing with `schedulefree.*` optimizers](https://github.com/argonne-lcf/Megatron-DeepSpeed/commit/aa2cd591cec5a355b59abd5ec248aed1f462f79f)
                - [Add support for `schedulefree.{AdamWScheduleFree,SGDScheduleFree}`](https://github.com/argonne-lcf/Megatron-DeepSpeed/commit/4e5c38321ca8d099b8bdad6fb0d47c54febd483e)

            - \[WIP\] [GaLore](github.com/jiaweizzhao/galore) with 8bit support
    - Downloaded + Tokenized latest release of Dolma dataset (v1.7) on both Polaris and Sunspot
    - Multiple meetings with team from Intel to discuss:
        - status of upcoming drop with fix for `flash-attn` on XPU
        - Experiments to run for benchmarking / profiling 70B + 1T model(s)

2. Blockers:
    - Waiting for Polaris upgrade to `CUDA=12.2` next week which should give performance improvements

</details>


<details closed><summary><b>[</b><code>2024-04-12</code><b>]</b></summary>

1. Updates:
    - Finished tokenization of Dolma dataset on Sunspot
    - Working with Intel to test new release of Flash Attention on Sunspot. 
        - Should close delta between loss curves previously seen with and without Flash Attn


2. Blockers:
    - Gordon Bell runs / effort on Polaris
 
</details>

<details closed><summary><b>[</b><code>2024-04-05</code><b>]</b></summary>

1. Updates:
    - **Convergence on XPU**
        - Identified ambiguity in optimizer creation that appeared to be impacting convergence on XPU
        - [Pushed fix](https://github.com/argonne-lcf/Megatron-DeepSpeed/commit/038109af825d62029f00c9717a2948b2adafa362) and tested / confirmed that loss curves match across {Polaris, Sunspot}

            <details closed><summary>Convergence Fix</summary>

            ![image](https://github.com/auroraGPT-ANL/training/assets/5234251/9d5e76c4-6416-4413-a51d-ae2a5143cc9e)

            </details>

        - Split up creation logic for creating different optimizers, [added support](https://github.com/argonne-lcf/Megatron-DeepSpeed/commit/5b9ad9a91d71c9b0573e6ba678ff1d2355a587f1) for `--optimizer={apex.adam, apex.sgd, torch.optim.Adam, torch.optim.AdamW}`

    - **Training on Sunspot**
        - New release of Dolma dataset broke our existing {download, tokenization} code
        - Patched our code to work with new version and download of full dataset (~5.6 TB) in process
    - **Training on Polaris**
        - Still working to confirm that our mechanism for skipping bad training steps is effective at preventing `NaN` values from back-propagating, resulting in a crash.
        - This is due in part to:
            - Efforts being refocused to fix apparent convergence issue on Sunspot, which is now complete.
            - The `argonne_tpc` project burned through its allocation on Polaris and jobs were being submitted to `backfill` queue 
                - [x] fixed as of 2024-04-04
            - Large queue depth on Polaris due to upcoming SC + GB deadlines

2. Blockers:
4. References:
5. Shoutouts:

</details>

## 2024-03

<details closed><summary><b>[</b><code>2024-03-29</code><b>]</b></summary>

- Updates:
    - Working on gathering performance measurements for Llama2-70B architecture on Polaris / Sunspot.
    - Ongoing effort to train full Llama-7B architecture with Dolma dataset on Polaris.
        - We observed that, shortly after the learning rate warmup completes, the loss curve begins to have significant spikes that cause the training procedure to crash with `NaN`. 
        - To mitigate this, we've implemented a mechanism for manually skipping the backpropagation update when this happens. If this method works effectively, we will automate it in the training pipeline.
    - Convergence issues on Aurora / Sunspot (PVC)
        - When training with identical configs on Polaris / Sunspot, we observed a disagreement in their loss curves. Specifically, we notice that the loss curve on PVC seems to plateau (as shown in the figure below).
        - Through an exhaustive debugging process, we were able to identify that the issue is resulting from an ambiguity in how Megatron-DeepSpeed creates the internal optimizer states. A method for resolving the issue has been proposed, and ongoing work to verify this is underway.
    - Training on Sunspot
        - In order to make progress while Aurora is unavailable we will continue pre-training on Sunspot. This requires creating (and tokenizing) an additional copy of the Dolma dataset on the `gila` filesystem. This is currently a work in progress.
- Blockers:
    - Jobs on Polaris have been slow to get through the queue due to the upcoming Gordon Bell submission deadline.
    - This has made it difficult to confirm the effectiveness of our "loss spike mitigation" technique, though tests have been ongoing at smaller scales.
    - Full scale pre-training on Sunspot had (previously) been blocked by the apparent convergence issue, and effort was re-focused to try and quickly tackle this issue.
        - We believe this issue has now been identified and a fix proposed. Once Sunspot is back online Monday, we will be able to perform these tests.
- References (links to any meeting notes, files, presentations to support
    - ![intel-convergence](./assets/intel-convergence-issue.png)
- Shoutouts (if you want):

</details>
