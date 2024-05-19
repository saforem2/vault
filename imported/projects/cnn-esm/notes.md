# `cnn4esm`

## TODO

> [!todo] TODO
> - [ ] Add forecasting methods for evaluating models trained on `.h5` datasets
> - [ ] Add / implement Romit's LSTM architecture from [`model_layersv2.py`](https://github.com/argonne-lcf/cnn-esm/blob/main/src/cnn4esm/network/tensorflow/model_layersv2.py)
> - [ ] Continue scaling up model architecture
> - [ ] Try running [`NVlabs/FourCastNet`](https://github.com/NVlabs/FourCastNet)
> 	- [ ] Look at [forecastNet/dataHelpers.py](https://github.com/jjdabr/forecastNet/blob/master/Pytorch/dataHelpers.py) and [ClimaX/src/climax/pretrain/dataset.py](https://github.com/microsoft/ClimaX/blob/main/src/climax/pretrain/dataset.py#L13) for guidance on data loader utilities

> [!done]- Completed
> - [x] Better communication in slack channel
> - [x] Integrate Chengming's new `.h5` `DataLoader` implementation into `cnn-esm` and test for OOM errors
> - [x] Depending on the success of the `h5Dataset` , decide on scheduling a meeting with Huihuo
> - [x] Ensure Chengming can run from `main` branch

> [!hint]- Groupings:
> ![](CleanShot%202023-03-31%20at%2012.50.19.png)


---
# Meeting notes

## 2023-04-24
	
### Notes
In  [`FourCastNet/utils/img_utils.py`](https://github.com/NVlabs/FourCastNet/blob/93360c1720a9f97aabf970689f21c9fad8737788/utils/img_utils.py#L88), they explicitly drop the last pixel:

```python
img = img[:, :, 0:720]  # remove last pixel
```

which is used in `FourCastNet/utils/data_loader_multifiles.py` in the [`GetDataset(Dataset)`](https://github.com/NVlabs/FourCastNet/blob/93360c1720a9f97aabf970689f21c9fad8737788/utils/data_loader_multifiles.py#L79) object


## 2023-04-21
- IO / Systems making progress towards identifying memory usage and profiling
- [ ] Gradient accumulation allowing for increased model capacity (~6x)
- [ ] Keep trainer.data.train_batch_size (here) constant and explicitly test gradient accumulation with DeepSpeed
- [ ] Explicitly test activation checkpointing with DeepSpeed
- [ ] NVlabs/FourCastNet
	- [ ] FourCastNet is based on the vision transformer architecture with Adaptive Fourier Neural Operator (AFNO) attention proposed in Guibas-Mardani et al. [paper], [code]

 - [ ] Sam Foreman / Troy to rewrite Trainer.make_data(batch) (from here)
	 - Need to decouple this reshaping / pre-processing logic from DataLoader objects
	 - Currently, we (for input_horizon = output_horizon = 1)
	 - Load batch.shape=(8, 21, 721, 1440) from .h5 file


## 2023-04-13
- [ ] Chengming will repeat profiling measurements to get statistics
- [ ] Sam will get Huihuo’s availability to discuss asynchronous data loader for early next week
- [ ] Will schedule deep dives with systems team and modeling team to iron out data loader / reshaping bugs

## 2023-04-13
- [ ] Get links to W&B runs from Troy for gradient_accumulation_steps comparison
- [ ] Get throughput measurements for recent experiments
- [ ] Chengming will work on getting detailed profiling results to understand where memory usage coming from at different points in forward / backward steps

## 2023-04-11 (systems sync)
- [ ] Talk to modeling team to identify optimal shuffling policy during training
- [ ] Sam to lead effort on organizing / coordinating efforts for IO / systems modeling
- [ ] Look at different optimization strategies 
- [ ] Work on collecting profiling results to look at IO bottlenecks
- [ ] Look at comparison with / without gradient accumulation
- [ ] Look at comparison with / without offloading
- [ ] Try different optimization / offloading strategies to enable larger model scaling
- [ ] Run profiling on multi-node jobs

## 2023-04-07
- [ ] Chengming will look at profiling and localization improvements
- [ ] Finalize time / date and request reservation on Polaris
- [ ] ==Increase model size / scale up architecture==

## 2023-04-04
### Updates
- Met with [@Charlie Zhou](https://deepspeed-anl-climate.slack.com/team/U04Q4PC72VB) and [@chengming.zhang](https://deepspeed-anl-climate.slack.com/team/U04Q12NMEMC) this morning to discuss the evaluation updates and to sync on current status of things.
- Over the weekend I added support for the multi-step-prediction / evaluation 
	- This gives us an indication of the models' performance shown in the plot below for `test/loss`
-   Throughput metric (`train/img_per_second` ) shown in the other plot below which is essentially (`world_size * batch_size / time_per_step`)

Additional items:  

-   [@Charlie Zhou](https://deepspeed-anl-climate.slack.com/team/U04Q4PC72VB) will continue working on adding support for the Vision Transformer
-   [@chengming.zhang](https://deepspeed-anl-climate.slack.com/team/U04Q12NMEMC) will look at data staging and adding the localization improvements
-   [@Troy Arcomano](https://deepspeed-anl-climate.slack.com/team/U04Q4PBL0ER) will build out the tools for generating plots (animations etc) from the `multi-step-prediction` / evaluation data
-   I will continue working on:

-   adding the multi-step-loss function as we discussed on Friday
-   adding / implementing [@Romit](https://deepspeed-anl-climate.slack.com/team/U04Q7J2R8HZ)’s `ConvLSTM2D` architecture in PyTorch and compare against current ResNet architecture

## 2023-03-31
- [ ] Add throughput `img / s` or similar metric that is independent of WORLD_SIZE, batch_size, etc
- [ ] Specific metrics required for GB submission (peak to peak performance etc)
	- [ ] Work with Minjia + Venkat to identify what specifically required
	- [ ] Relatively 

> [!success]  Changes from this week
> - [x] Implemented [standardization](https://github.com/argonne-lcf/cnn-esm/blob/d3fb9e0b7d2f26d3a5b1f90fd6b7313c3eb42e74/src/cnn4esm/datasets/hdf5.py#L89) in `h5Dataset` from `src/cnn4esm/datasets/hdf5.py`
> - [x] Updated [README]('https://github.com/argonne-lcf/cnn-esm)
> - [x] Added bash scripts
> 	- [cnn-esm/src/cnn4esm/bin/train.sh](https://github.com/argonne-lcf/cnn-esm/blob/main/src/cnn4esm/bin/train.sh)
> - [x] Added logic for standardizing data at beginning of training using global statistics e.g. `x = (x - μ) / σ`
> - [x] Adds Romit's `network/tensorflow/model_layersv2.py`
> - Additional changes:
> 	- [x] Clearer logic for checkpointing / restoring from checkpoint
> 	- [x] Adds switch for `network.use_large_resnet: bool`
> 	- [x] Remove unused `timestep` from `h5Dataset` in `datasets/hdf5.py`
>

```Shell
   File "/lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/cnn-esm/venvs/polaris/2023-01-10/lib/python3.10/site-packages/deepspeed/runtime/zero/stage3.py", line 2123, in state_dict
    raise NotImplementedError(
NotImplementedError: ZeRO-3 does not yet support checkpointing with NVMe offloading, please disable for now.
```









- Sync w/ Leon + Chengming
	- Leon has google doc with status updates ??
	- Send an update with description of current script 
	- Recent changes / status of everything
	- Create google doc
	- `ZeRO.stage = 1`:
		- [x] `batch_size = 8` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-121318/workspace?workspace=user-saforem2)
		- [x] `batch_size = 16` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-122456/workspace?workspace=user-saforem2)
		- [x] `batch_size = 24` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-123622/workspace?workspace=user-saforem2)
		- [!] `batch_size=32` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-124617?workspace=user-saforem2)
	- `ZeRO.stage = 2`:
		- [x] `batch_size = 8` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/runs/wl4r1ty6/overview?workspace=user-saforem2)
		- [x] `batch_size = 16` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-122456/workspace?workspace=user-saforem2)
		- [x] `batch_size = 24` [(W&B Run)](https://wandb.ai/l2hmc-qcd/cnn-esm/groups/experiment-20230331-123622/workspace?workspace=user-saforem2)
	- From google doc:
		 - Attendees:
			 - Sam, Chengming, Leon
		 - Prepare high-level overview for meeting today:
			 - Status of script
			 - Current functionality
			 - Changes over past week
		 - Chengming will prepare slides for larger group meeting
		 - Locality aware functionality
		 - Determine / explain Polaris hardware for
			 - Data staging
			 - NVME offloading
				 - Polaris: /local/scratch
				 - ThetaGPU: /raid/scratch
		 - Ask about fp16 training, when specifying fp16 does this carry over to activation precision ?
		 - Try scaling up batch size?
			 - Determine largest possible batch sizes for different ZeRO stage and offloading
			 - Be careful about precision=fp16 
			 - Sam will run different combos of batch size vs ZeRO stage
				 - Try to find largest possible batch size for each ZeRO stage / offloading combo 
			 - Zero = 1:
			 - Zero = 2 no offloading:
				 - Largest batch size: 8 (chengming)
			 - Zero = 2 w/ offloading (CPU):
				 - Largest batch size: 24 (sam) (CONFIRM)
			 - Zero 3:
				 - CPU:
					 - Largest batch size: XXX
				 - NVME:
					 - Largest batch size: XXX
		 - Add metrics for throughput calculations (img / sec)
			 - Optimize for throughput
				 - Balance between offloading and performance
			 - Try different combinations and look for sweet spot between offloading and throughput
		 - Chengming will prepare overview of
			 - Localization strategies
			 - Load balancing from IO staging
			 - Will prepare slides
		 - Look into IO staging on Polaris
			 - Identify RW latency, bandwidth, hardware specifics
			 - Design staging strategy depending on ^
			 - `mpirun cp -r /eagle/MDClimSim/troyarcomano/train/*.h5 /local/scratch/`
		    
		
	

- Sync w/ Troy:
	- Add Troy's fix in `ResNetBlock` 

# 2023-03-28
- [ ] Continue meeting / working closely with Chengming
- [ ] Check in on Chengming regularly
- [ ] Send https://github.com/argonne-lcf/cnn-esm/blob/main/src/cnn4esm/conf/ds_config.json
- [ ] Ask Rao to start downloading data

## 2023-03-27
- [ ] Romit has working LSTM in TensorFlow
- [ ] Add $\alpha \propto \sqrt{N} \alpha_{0}$ for scaling learning rate by `sqrt(WORLD_SIZE)`
- [ ] Troy working on forecasting metrics for comparison
- [ ] `LRScheduler` 
	- [ ] DeepSpeed cosine annealing
	- [ ] WarmupDecayLR
	- [ ] Try naive scheduling to make sure training stable / no exploding gradients
- [ ] Regularization
	- [ ] Romit / Troy looked at adding L1, L2 Regularization previously
	- [ ] Gradient clipping
- [ ] Weight Initialization
	- [ ] smaller $\sigma$ in weights $\propto$ size of hidden layer

- [ ] Chengming Charlie Chong Zhou

## 2023-03-24
- [x] Work with Chengming to figure out logging / printing issues
- [-] Meet w/ Huihuo + Chengming about IO / HDF5 issues **early next week**

## 2023-03-21
- [x] Remove MinMaxScaler from `main` branch
- [x] Global `.h5` file with different workers grabbing from global dataset using indices determined by random seed

---
- Meeting today w/ Leon + DeepSpeed team (SC GB24)
- Try adding gradient clipping to fix spike in training loss
- 2 failure modes:
	- saturating, flattening out
	- spike
- 1 step input, 1 step output
- 1 time step into the future


---

# Inference Shape Bug

We have:
```python
train_data.shape = [668, 11, 256, 128]  # = [668, C, H, W]
val_data.shape = [75, 11, 256, 128]     # = [75, C, H, W]
```

we split this into

```python
  # 32 batches of size: [20 (= 668 / 32), C, W, H]
```

i.e.
```Python
train_data = [
    batch1,   # shape = [20, C, W, H]
    batch2,   # shape = [20, C, W, H],
    ...,    
    batch32,  # shape = [20, C, W, H],
]
```
for a single batch, we split it as input / output by

```python

def make_data(data: torch.Tensor) -> tuple[torch.Tensor, torch.Tensor]:
	"""Split data as (input, output) pair.

	NOTE: We assume data in CHANNELS_FIRST format, [N, C, H, W]
	"""
	nd0, nd1 = data.shape[2], data.shape[3]
	end_time = (
	    self.config.input_horizon     # e.g. 8
	    + self.config.output_horizon  # e.g. 8
	)
	i = 0
	input_data = []
	output_data = []
	while i < (data.shape[0] - end_time):
		# Example:
		#  - iH : input horizon
		#  - oH : output horizon
		# --------
		# inp = [
		#     data[0:iH],
		#     data[1:(1+iH)],
		#     data[2:(2+iH)],
		#     ...,
		# ]
	    # outp = [
	    #     data[iH:(iH+oH)],
	    #     data[(1+iH):(1+oH)],
	    #     data[(2+iH):(2+oH)],
	    #     ...,
	    # ]
	    inp = data[
	        i:(i + self.config.input_horizon)
	    ]
	    outp = data[
	    	(i + self.config.input_horizon):(i + end_time)
	    ]
	    input_data.append(inp.reshape(-1, nd0, nd1))
	    output_data.append(outp.reshape(-1, nd0, nd1))
		i += 1
```

if the input `data` to the `make_data` function above has shape `data.shape = [20, 11, 256, 128]`, for example, we would construct `input_data` and `output_data` as 

```python
>>> data.shape
[20, 11, 256, 128]
>>> data.shape[0] - end_time  # (20 - 16)
4
>>> # input_data, output_data = make_data(data) 
>>> input_data = [
>>>     data[0:8],
>>>     data[1:9],
>>>     data[2:10],
>>>     data[3:11]
>>> ]
>>> output_data = [
>>>     data[8:16],
>>>     data[9:17],
>>>     data[10:18],
>>>     data[11:19],
>>> ]
```

- **Issue**: 
	- However, when trying to build a _validation_ batch, our `val_data.shape = [75, 11, 256, 128]`, which we split into 32 batches, each of shape `[2, 11, 256, 128]`, e.g.
	```python
	val_data = [
		val_batch1,   # shape: [2, 11, 256, 128]
		val_batch2,   # shape: [2, 11, 256, 128]
		...,
		val_batch32,  # shape: [2, 11, 256, 128]
    ]
	```
	since `val_batch.shape[0] = 2`, trying to split it into `input_data`, `output_data` like above causes an error