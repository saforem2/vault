# LLMs on AI Accelerators

## 2023-05-10
- [ ] Re-run `1.5B` model on Polaris w/ `saforem2/Megatron-DeepSpeed`
	- [ ] Try w/ `seq_len = {1024,2048}`
	- [ ] Multiple runs to gather statistics
	- [ ] try w/ different `micro_batch`, `grad_accumulation_steps`, `MPSIZE`, etc.
	- [ ] Start from best settings for `25B` model
	- [ ] _then_ look at scaling study (1 → 2 → 4 → ...)
- [ ] Update working draft on [Overleaf](https://www.overleaf.com/project/6437e62ceed37522113547e5)
	- [ ] Add text describing `GenSLM` + differences between `Megatron-DeepSpeed` w/ `GenSLM` data vs. [`ramanathanlab/genslm-develop`](https://github.com/ramanathanlab/genslm-develop)
	- [/] Focus on getting results from `Megatron-DeepSpeed` from W&B
	- [ ] Add text about Megatron-DeepSpeed Implementation & experiments on NVIDIA A100's (Polaris @ ALCF)

