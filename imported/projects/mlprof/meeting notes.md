# [`argonne-lcf/mlprof`](https://github.com/argonne-lcf/mlprof)

- [ ] MPI Profiling to get all collective comm. ops with same model across all backends (Horovod, DDP, DeepSpeed)
	-  Reference: [Profiling](https://github.com/argonne-lcf/mlprof#profiling) using `libmpitrace.so` on Polaris
- [ ] Start with `2` nodes initially then scale with increasing number of nodes
- [ ] Get profiles for DeepSpeed ZeRO 1, 2, 3 and Mixture of experts (MoE)
- [ ] Identify what parameters can impact performance such as NCCL environment variables and framework specific parameters
- [ ] Do the analysis for standard models and LLMs
- [ ] Develop auto-tuning methods to set these parameters for optimal performance

## 2023-02-20

- [ ] Group `mpiprofile`'s with the associated runs' log
	- [ ] Make clear what backend used + group by backend
- [ ] Scale up message sizes in `mpiprofiles`
- [ ] Aggregate into table, **grouped by backend**
- [ ] Ensure all GPUs being utilized
	- [ ] Should be fixed in `conda/2023-01-10` on Polaris
	- [ ] Bug in `conda/2022-09-08-hvd-nccl` that causes all processes to be mapped to GPU0 for some reason
