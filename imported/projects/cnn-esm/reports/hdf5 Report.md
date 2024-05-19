# `hdf5` Report
---
author: Sam Foreman
title: h5Dataset-OOM
date: 2023-03-26
---

# OOM Errors with `h5Dataset`

## Summary

Below we walk through the steps of loading / preprocessing data and building / instantiating our Trainer object.

Briefly, we:

1. Instantiate `TrainerConfig`

    - Instantiate `npconfig` and `h5config` (both type: `TrainerConfig`) objects
        by passing `overrides: list[str]` to the `get_config` method from
        [`configs.py`](../src/cnn4esm/configs.py)

    - By changing `use_hdf5=True | False` in `overrides`, can specify whether we
        want to use the [`h5Dataset`](../src/cnn4esm/datasets/hdf5.py) or
        [`npDataset`](../src/cnn4esm/datasets/numpy.py) dataset object

2. Load / preprocess data

    - Using the `setup_data(rank: int | str, config:
        TrainerConfig)` function from
        [`../src/cnn4esm/datasets/utils.py`](../src/cnn4esm/datasets/utils.py) to
        build our [`Data`](../src/cnn4esm/configs.py#L104) objects

3. Build a [`Trainer(config: TrainerConfig, data:
   Data)`](../src/cnn4esm/trainer/pytorch/trainer.py) object, and try running a
   single training step.

     - We can see in `In[21]:` below that our `nptrainer`  is able to run a
         training step successfully

     - whereas our `h5trainer` object crashes with OOM error in `In[22]:`

> **Note**<br>
> - Note that we are able to load and iterate through the `DataLoader` object:
>     - `h5Dataset`: `In[19]:`
>     - `npDataset`: `In[20]:`
>
>   but we only run into the OOM performing a training step with the `h5Dataset`


## Results

```python
In [1]: %load_ext autoreload
   ...: %autoreload 2
   ...: from cnn4esm.datasets.numpy import npDataset ; from cnn4esm.datasets.hdf5 import h5Dataset
   ...: from cnn4esm.datasets.utils import load_npdata, setup_data, setup_datasets, setup_h5data, setup_npdata, get_h5files
   ...: from cnn4esm.configs import get_config
   ...: npconfig = get_config(overrides=['backend=DDP', 'use_hdf5=False', 'precision=fp16', 'timestep=1'])
   ...: h5config = get_config(overrides=['backend=DDP', 'max_files=2', 'use_hdf5=True', 'precision=fp16', 'val_years=[]', 'test_years=[]', 'timestep=1'])
   ...: npdata = setup_data(0, npconfig)
   ...: h5data = setup_data(0, h5config)
# ----------------------------------------------------
# numpy data, show info during reshaping operation
input_total.shape [N, H, W, C]: (2972, 256, 128, 11)
input_total.shape [N, C, H, W]: (2972, 11, 256, 128)
train.shape: (1671, 11, 256, 128)
val.shape: (558, 11, 256, 128)
test.shape: (743, 11, 256, 128)
# ----------------------------------------------------
# h5 data, skipping loading any val / test data
# due to OOM errors
No val dset! Skipping!!
No test dset! Skipping!!
# ----------------------------------------------------

In [2]: npdata.train.dataset.shape
Out[2]: (1671, 11, 256, 128)

In [3]: h5data.train.dataset.shape
Out[3]: (1460, 21, 721, 1440)

In [4]: xnp = next(iter(npdata.train.loader))

In [5]: xh5 = next(iter(h5data.train.loader))

In [6]: xnp.shape
Out[6]: torch.Size([32, 11, 256, 128])

In [7]: xh5.shape
Out[7]: torch.Size([32, 21, 721, 1440])

In [8]: from cnn4esm.trainer.pytorch.trainer import Trainer

In [9]: nptrainer = Trainer(config=npconfig, data=npdata)

In [10]: h5trainer = Trainer(config=h5config, data=h5data)

In [11]: bh5 = next(iter(h5trainer.data.train.loader))

In [12]: bnp = next(iter(nptrainer.data.train.loader))

In [13]: bnp.shape
Out[13]: torch.Size([32, 11, 256, 128])

In [14]: bh5.shape
Out[14]: torch.Size([32, 21, 721, 1440])

In [15]: xnp, ynp = nptrainer.make_data(bnp)

In [16]: xh5, yh5 = h5trainer.make_data(bh5)

In [17]: xh5.shape
Out[17]: torch.Size([16, 168, 721, 1440])


In [18]: h5trainer.device
Out[18]: 'cuda'

In [19]: import time
    ...:
    ...: t0 = time.time()
    ...: for i, b in enumerate(h5trainer.data.train.loader):
    ...:     print(f'{i}: batch.shape: {b.shape}')
    ...:     x, y = h5trainer.make_data(b)
    ...:     print(f'input.shape: {x.shape}, output.shape: {y.shape}')
    ...:     if i > 5:
    ...:         break
    ...: print(f'took: {time.time() - t0:.6f}s')
0: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
1: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
2: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
3: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
4: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
5: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
6: batch.shape: torch.Size([32, 21, 721, 1440])
input.shape: torch.Size([16, 168, 721, 1440]), output.shape: torch.Size([16, 168, 721, 1440])
took: 9.494975s

In [20]: import time
    ...:
    ...: t0 = time.time()
    ...: for i, b in enumerate(nptrainer.data.train.loader):
    ...:     print(f'{i}: batch.shape: {b.shape}')
    ...:     x, y = h5trainer.make_data(b)
    ...:     print(f'input.shape: {x.shape}, output.shape: {y.shape}')
    ...:     if i > 5:
    ...:         break
    ...: print(f'took: {time.time() - t0:.6f}s')
0: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
1: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
2: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
3: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
4: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
5: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
6: batch.shape: torch.Size([32, 11, 256, 128])
input.shape: torch.Size([16, 88, 256, 128]), output.shape: torch.Size([16, 88, 256, 128])
took: 0.258170s

In [21]: nploss = nptrainer.train_step(xnp, ynp)

In [22]: h5loss = h5trainer.train_step(xh5, yh5)
r"""---------------------------------------------------------------------------
OutOfMemoryError                          Traceback (most recent call last)
Cell In[22], line 1
----> 1 h5loss = h5trainer.train_step(xh5, yh5)

File /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/cnn-esm/src/cnn4esm/trainer/pytorch/trainer.py:435, in Trainer.train_step(self, x, y)
    433 self.optimizer.zero_grad()
    434 with self.autocast_context:
--> 435     loss = self.get_loss(x, y)
    436 if (
    437         self.model_engine is not None
    438         and self.config.backend.lower() in ['ds', 'deepspeed']
    439 ):
    440     self.model_engine.backward(loss)  # type:ignore

File /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/cnn-esm/src/cnn4esm/trainer/pytorch/trainer.py:330, in Trainer.get_loss(self, x, y)
    323 def get_loss(
    324         self,
    325         x: torch.Tensor,
    326         y: torch.Tensor
    327 ) -> torch.Tensor:
    328     z = (
    329         self.model(x) if self.model_engine is None
--> 330         else self.model_engine(x)
    331     )
    332     return ((z - y) ** 2).mean()

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/module.py:1194, in Module._call_impl(self, *input, **kwargs)
   1190 # If we don't have any hooks, we want to skip the rest of the logic in
   1191 # this function, and just call forward.
   1192 if not (self._backward_hooks or self._forward_hooks or self._forward_pre_hooks or _global_backward_hooks
   1193         or _global_forward_hooks or _global_forward_pre_hooks):
-> 1194     return forward_call(*input, **kwargs)
   1195 # Do not call functions when jit is used
   1196 full_backward_hooks, non_full_backward_hooks = [], []

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/parallel/distributed.py:1040, in DistributedDataParallel.forward(self, *inputs, **kwargs)
   1036 if self._join_config.enable:
   1037     # Notify joined ranks whether they should sync in backwards pass or not.
   1038     self._check_global_requires_backward_grad_sync(is_joined_rank=False)
-> 1040 output = self._run_ddp_forward(*inputs, **kwargs)
   1042 # sync params according to location (before/after forward) user
   1043 # specified as part of hook, if hook was specified.
   1044 if self._check_sync_bufs_post_fwd():

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/parallel/distributed.py:1003, in DistributedDataParallel._run_ddp_forward(self, *inputs, **kwargs)
   1001 else:
   1002     with self._inside_ddp_forward():
-> 1003         return module_to_run(*inputs, **kwargs)

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/module.py:1194, in Module._call_impl(self, *input, **kwargs)
   1190 # If we don't have any hooks, we want to skip the rest of the logic in
   1191 # this function, and just call forward.
   1192 if not (self._backward_hooks or self._forward_hooks or self._forward_pre_hooks or _global_backward_hooks
   1193         or _global_forward_hooks or _global_forward_pre_hooks):
-> 1194     return forward_call(*input, **kwargs)
   1195 # Do not call functions when jit is used
   1196 full_backward_hooks, non_full_backward_hooks = [], []

File /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/cnn-esm/src/cnn4esm/network/pytorch/network.py:210, in cnnESM.forward(self, x)
    208 x = x.to(self.device)
    209 for block in self.layers:
--> 210     x = block(x)
    211 return x

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/module.py:1194, in Module._call_impl(self, *input, **kwargs)
   1190 # If we don't have any hooks, we want to skip the rest of the logic in
   1191 # this function, and just call forward.
   1192 if not (self._backward_hooks or self._forward_hooks or self._forward_pre_hooks or _global_backward_hooks
   1193         or _global_forward_hooks or _global_forward_pre_hooks):
-> 1194     return forward_call(*input, **kwargs)
   1195 # Do not call functions when jit is used
   1196 full_backward_hooks, non_full_backward_hooks = [], []

File /lus/grand/projects/datascience/foremans/locations/polaris/projects/argonne-lcf/cnn-esm/src/cnn4esm/network/pytorch/network.py:96, in ResNetBlockSmall.forward(self, x)
     94 def forward(self, x: torch.Tensor):
     95     x.to(self.device)
---> 96     x1 = self.activation(self.main_layer(x))
     97     x1 = self.padding(x1)
     98     x2 = self.skip_layer(x)

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/module.py:1194, in Module._call_impl(self, *input, **kwargs)
   1190 # If we don't have any hooks, we want to skip the rest of the logic in
   1191 # this function, and just call forward.
   1192 if not (self._backward_hooks or self._forward_hooks or self._forward_pre_hooks or _global_backward_hooks
   1193         or _global_forward_hooks or _global_forward_pre_hooks):
-> 1194     return forward_call(*input, **kwargs)
   1195 # Do not call functions when jit is used
   1196 full_backward_hooks, non_full_backward_hooks = [], []

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/conv.py:463, in Conv2d.forward(self, input)
    462 def forward(self, input: Tensor) -> Tensor:
--> 463     return self._conv_forward(input, self.weight, self.bias)

File /soft/datascience/conda/2023-01-10/mconda3/lib/python3.10/site-packages/torch/nn/modules/conv.py:459, in Conv2d._conv_forward(self, input, weight, bias)
    455 if self.padding_mode != 'zeros':
    456     return F.conv2d(F.pad(input, self._reversed_padding_repeated_twice, mode=self.padding_mode),
    457                     weight, bias, self.stride,
    458                     _pair(0), self.dilation, self.groups)
--> 459 return F.conv2d(input, weight, bias, self.stride,
    460                 self.padding, self.dilation, self.groups)

OutOfMemoryError: CUDA out of memory. Tried to allocate 5.18 GiB (GPU 0; 39.59 GiB total capacity; 28.93 GiB already allocated; 1.58 GiB free; 36.41 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF
```

