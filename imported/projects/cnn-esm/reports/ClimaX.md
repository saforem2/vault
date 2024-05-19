# ClimaX implementation

- Added in `network/pytorch/climax.py`
- Status:
	- OOM for full-sized (`[21, 721, 1440]`) images
	- Works for small images (tested on `[21, 128, 256]`, shown below)
 
```python
In [1]: %load_ext autoreload

In [2]: %autoreload 2

In [3]: from cnn4esm.configs import get_config
   ...: from cnn4esm.io.utils import setup_data
   ...: from cnn4esm.trainer.pytorch.trainer import Trainer
   ...: config = get_config(
   ...:     overrides=[
   ...:         'backend=DDP',
   ...:         'use_wandb=False',
   ...:         'precision=fp16',
   ...:         'network.nlayers=10',
   ...:         'network.layer_size=128',
   ...:         'trainer.max_global_steps=500',
   ...:         'trainer.print_steps=10',
   ...:         'data.gradient_accumulation_steps=1',
   ...:         'data.train_batch_size=1',
   ...:         'verbose=true',
   ...:     ]
   ...: )
   ...: data = setup_data(0, config=config.data)
   ...: trainer = Trainer(config=config, data=data)

/lus/eagle/projects/MDClimSim/foremans/cnn-esm/src/cnn4esm/configs.py:597: UserWarning:
The version_base parameter is not specified.
Please specify a compatability version level, or None.
Will assume defaults for version 1.1
  with initialize_config_dir(
[05/15/23 11:52:29] WARNING  Global batch size not specified!
[05/15/23 11:52:29] WARNING  Computing as: train_batch_size * gradient_accumulation_steps * world_size = 1 * 1 * 1 = 1
[05/15/23 11:52:29] INFO     h5Dataset.shape: (1460, 21, 721, 1440)
[05/15/23 11:52:29] INFO     h5Dataset.file_list: ['/eagle/MDClimSim/troyarcomano/train/1979.h5', '/eagle/MDClimSim/troyarcomano/train/1980.h5', '/eagle/MDClimSim/troyarcomano/train/1981.h5', '/eagle/MDClimSim/troyarcomano/train/1982.h5',
                             '/eagle/MDClimSim/troyarcomano/train/1983.h5', '/eagle/MDClimSim/troyarcomano/train/1984.h5', '/eagle/MDClimSim/troyarcomano/train/1985.h5', '/eagle/MDClimSim/troyarcomano/train/1986.h5',
                             '/eagle/MDClimSim/troyarcomano/train/1987.h5', '/eagle/MDClimSim/troyarcomano/train/1988.h5', '/eagle/MDClimSim/troyarcomano/train/1989.h5', '/eagle/MDClimSim/troyarcomano/train/1990.h5',
                             '/eagle/MDClimSim/troyarcomano/train/1991.h5', '/eagle/MDClimSim/troyarcomano/train/1992.h5', '/eagle/MDClimSim/troyarcomano/train/1993.h5', '/eagle/MDClimSim/troyarcomano/train/1994.h5',
                             '/eagle/MDClimSim/troyarcomano/train/1995.h5', '/eagle/MDClimSim/troyarcomano/train/1996.h5', '/eagle/MDClimSim/troyarcomano/train/1997.h5', '/eagle/MDClimSim/troyarcomano/train/1998.h5',
                             '/eagle/MDClimSim/troyarcomano/train/1999.h5', '/eagle/MDClimSim/troyarcomano/train/2000.h5', '/eagle/MDClimSim/troyarcomano/train/2001.h5', '/eagle/MDClimSim/troyarcomano/train/2002.h5',
                             '/eagle/MDClimSim/troyarcomano/train/2003.h5', '/eagle/MDClimSim/troyarcomano/train/2004.h5', '/eagle/MDClimSim/troyarcomano/train/2005.h5', '/eagle/MDClimSim/troyarcomano/train/2006.h5',
                             '/eagle/MDClimSim/troyarcomano/train/2007.h5', '/eagle/MDClimSim/troyarcomano/train/2008.h5', '/eagle/MDClimSim/troyarcomano/train/2009.h5', '/eagle/MDClimSim/troyarcomano/train/2010.h5',
                             '/eagle/MDClimSim/troyarcomano/train/2011.h5', '/eagle/MDClimSim/troyarcomano/train/2012.h5', '/eagle/MDClimSim/troyarcomano/train/2013.h5']

[05/15/23 11:52:29] INFO     h5Datasets.len(tile_ids): 25550
[05/15/23 11:52:29] INFO     h5Dataset.num_tiles_per_year = 730
[05/15/23 11:52:29] INFO     h5Dataset.shape: (1460, 21, 721, 1440)
[05/15/23 11:52:29] INFO     h5Dataset.file_list: ['/eagle/MDClimSim/troyarcomano/train/2014.h5']
[05/15/23 11:52:29] INFO     h5Datasets.len(tile_ids): 730
[05/15/23 11:52:29] INFO     h5Dataset.num_tiles_per_year = 730
[05/15/23 11:52:29] INFO     h5Dataset.shape: (1460, 21, 721, 1440)
[05/15/23 11:52:29] INFO     h5Dataset.file_list: ['/eagle/MDClimSim/troyarcomano/train/2015.h5']
[05/15/23 11:52:29] INFO     h5Datasets.len(tile_ids): 730
[05/15/23 11:52:29] INFO     h5Dataset.num_tiles_per_year = 730
[05/15/23 11:52:29] INFO     Caught MASTER_PORT:2345 from environment!
/lus/theta-fs0/software/thetagpu/conda/2023-01-11/mconda3/lib/python3.10/site-packages/torch/nn/modules/lazy.py:180: UserWarning: Lazy modules are a new feature under heavy development so changes to the API or functionality can happen at any moment.
  warnings.warn('Lazy modules are a new feature under heavy development '
[05/15/23 11:52:29] INFO     num_params in model: 1535374
[05/15/23 11:52:29] INFO     Using torch.autocast(torch.float16, cuda)
[05/15/23 11:52:29] INFO     Model: cnnESM(
                               (layers): ModuleList(
                                 (0): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(21, 21, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(21, 21, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (1): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(21, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(21, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (2): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (3): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (4): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (5): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (6): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (7): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (8): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (9): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (10): ResNetBlockSmall(
                                   (activation): ReLU(inplace=True)
                                   (main_layer): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                                 (11): ResNetBlockSmall(
                                   (activation): Identity()
                                   (main_layer): Conv2d(128, 21, kernel_size=(3, 3), stride=(1, 1))
                                   (skip_layer): Conv2d(128, 21, kernel_size=(1, 1), stride=(1, 1))
                                   (padding): PeriodicPadding()
                                 )
                               )
                             )
[05/15/23 11:52:29] INFO     Saving outputs in: /lus/eagle/projects/MDClimSim/foremans/cnn-esm/src/cnn4esm

In [4]: from cnn4esm.network.pytorch.climax import ClimaX
    ...: kwargs_small = {
    ...:     'img_size': [128, 256],
    ...:     'patch_size': 2,
    ...:     'embed_dim': 128,
    ...:     'depth': 2,
    ...:     'decoder_depth': 1,
    ...:     'num_heads': 2,
    ...:     'mlp_ratio': 4.0,
    ...:     'drop_path': 0.1,
    ...:     'drop_rate': 0.1,
    ...: }
    ...: climax_small = ClimaX(**kwargs_small)

In [5]: climax_small.cuda()
Out[5]:
ClimaX(
  (token_embeds): ModuleList(
    (0): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (1): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (2): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (3): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (4): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (5): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (6): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (7): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (8): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (9): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (10): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (11): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (12): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (13): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (14): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (15): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (16): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (17): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (18): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (19): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
    (20): PatchEmbed(
      (proj): Conv2d(1, 128, kernel_size=(2, 2), stride=(2, 2))
      (norm): Identity()
    )
  )
  (var_agg): MultiheadAttention(
    (out_proj): NonDynamicallyQuantizableLinear(in_features=128, out_features=128, bias=True)
  )
  (lead_time_embed): Linear(in_features=1, out_features=128, bias=True)
  (pos_drop): Dropout(p=0.1, inplace=False)
  (blocks): ModuleList(
    (0): Block(
      (norm1): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn): Attention(
        (qkv): Linear(in_features=128, out_features=384, bias=True)
        (attn_drop): Dropout(p=0.0, inplace=False)
        (proj): Linear(in_features=128, out_features=128, bias=True)
        (proj_drop): Dropout(p=0.1, inplace=False)
      )
      (ls1): Identity()
      (drop_path1): Identity()
      (norm2): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (mlp): Mlp(
        (fc1): Linear(in_features=128, out_features=512, bias=True)
        (act): GELU(approximate='none')
        (drop1): Dropout(p=0.1, inplace=False)
        (fc2): Linear(in_features=512, out_features=128, bias=True)
        (drop2): Dropout(p=0.1, inplace=False)
      )
      (ls2): Identity()
      (drop_path2): Identity()
    )
    (1): Block(
      (norm1): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (attn): Attention(
        (qkv): Linear(in_features=128, out_features=384, bias=True)
        (attn_drop): Dropout(p=0.0, inplace=False)
        (proj): Linear(in_features=128, out_features=128, bias=True)
        (proj_drop): Dropout(p=0.1, inplace=False)
      )
      (ls1): Identity()
      (drop_path1): DropPath(drop_prob=0.100)
      (norm2): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
      (mlp): Mlp(
        (fc1): Linear(in_features=128, out_features=512, bias=True)
        (act): GELU(approximate='none')
        (drop1): Dropout(p=0.1, inplace=False)
        (fc2): Linear(in_features=512, out_features=128, bias=True)
        (drop2): Dropout(p=0.1, inplace=False)
      )
      (ls2): Identity()
      (drop_path2): DropPath(drop_prob=0.100)
    )
  )
  (norm): LayerNorm((128,), eps=1e-05, elementwise_affine=True)
  (head): Sequential(
    (0): Linear(in_features=128, out_features=128, bias=True)
    (1): GELU(approximate='none')
    (2): Linear(in_features=128, out_features=84, bias=True)
  )
)

In [6]: x, y = next(iter(trainer.train_loader))

In [7]: x = x.to(trainer._dtype).to(trainer.device)
	
In [8]: y = y.to(trainer._dtype).to(trainer.device)

In [9]: x.device, x.dtype
Out[10]: (device(type='cuda', index=0), torch.float16)

In [11]: x_ = x[:, :, :128, :256]

In [12]: x_.shape
Out[12]: torch.Size([1, 21, 128, 256])

In [13]: preds_cx = climax_small(x_)
```