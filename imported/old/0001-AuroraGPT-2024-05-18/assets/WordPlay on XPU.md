.minimal-code-scroll .HyperMD-codeblock.HyperMD-codeblock-bg {

1. [ ]  overflow-y: scroll;
2. [ ]  /* white-space: pre; */

1. /* white-space-collapse: preserve; */
2. /* text-wrap: nowrap; */

}---
"cssclasses:":
  - max
---
# WordPlay on XPU

## Convergence Testing

### ✅ WORKING on CPU

- `TORCH_DEVICE="cpu"` works  !! in a single process:

    ```bash
    $ TORCH_DEVICE="cpu" python3 __main__.py +experiment=shakespeare data=shakespeare train.dtype=fp32 train.backend=DDP train.max_iters=1000 train.log_interval=10 train.compile=false                            
    ```
    
  - W&B Run: [whole-dust-173](https://wandb.ai/aurora_gpt/WordPlay/runs/ytmvfeup/workspace?nw=nwuserforemans)
      ![md](0005-Work/0001-AuroraGPT/assets/ScreenShot-2024-03-22-101557@2x.png)

### 🐛 Fails on XPU

- `TORCH_DEVICE="xpu"` crashes with `RuntimeError: tensor doese not have a device`, e.g.:

    - When running in `pdb`:
    
        ```bash
        (Pdb) self.model.to("xpu")
        GPT(
          (transformer): ModuleDict(
            (wte): Embedding(65, 384)
            (wpe): Embedding(256, 384)
            (drop): Dropout(p=0.2, inplace=False)
            (h): ModuleList(
              (0-5): 6 x Block(
                (ln_1): LayerNorm()
                (attn): CausalSelfAttention(
                  (c_attn): Linear(in_features=384, out_features=1152, bias=False)
                  (c_proj): Linear(in_features=384, out_features=384, bias=False)
                  (attn_dropout): Dropout(p=0.2, inplace=False)
                  (resid_dropout): Dropout(p=0.2, inplace=False)
                )
                (ln_2): LayerNorm()
                (mlp): MLP(
                  (c_fc): Linear(in_features=384, out_features=1536, bias=False)
                  (act_fn): GELU(approximate='none')
                  (c_proj): Linear(in_features=1536, out_features=384, bias=False)
                  (dropout): Dropout(p=0.2, inplace=False)
                )
              )
            )
            (ln_f): LayerNorm()
          )
          (lm_head): Linear(in_features=384, out_features=65, bias=False)
        )
        (Pdb) self.optimizer.zero_grad()
        (Pdb) x = x.to("xpu")
        (Pdb) y = y.to("xpu")
        (Pdb) with torch.xpu.amp.autocast(enabled=True, dtype=torch.bfloat16): logits, loss = self.model_engine(x, y)
        (Pdb) loss
        tensor(4.2439, device='xpu:0', grad_fn=<NllLossBackward0>)
        (Pdb) loss.backward()
        *** RuntimeError: tensor does not have a device
        ```

    - When running as a job:
            
        ```bash
        Error executing job with overrides: ['+experiment=shakespeare', 'data=shakespeare', 'train.dtype=bf16', 'train.backend=DDP', 'train.max_iters=1000', 'train.log_interval=10', 'train.compile=false']
        Traceback (most recent call last):
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/wordplay/src/wordplay/__main__.py", line 159, in main
            return train(cfg)
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/wordplay/src/wordplay/__main__.py", line 139, in train
            trainer.train()
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/ezpz/src/ezpz/dist.py", line 89, in wrapper
            result = func(*args, **kwargs)
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/wordplay/src/wordplay/trainer.py", line 879, in train
            output = self.train_step(x=output['x'], y=output['y'])
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/wordplay/src/wordplay/trainer.py", line 765, in train_step
            dtb_ = self._backward_step(
          File "/lus/gila/projects/Aurora_deployment/foremans/locations/sunspot/projects/saforem2/wordplay/src/wordplay/trainer.py", line 652, in _backward_step
            loss.backward()
          File "/home/foremans/miniconda3/envs/q4-drop/lib/python3.9/site-packages/torch/_tensor.py", line 492, in backward
            torch.autograd.backward(
          File "/home/foremans/miniconda3/envs/q4-drop/lib/python3.9/site-packages/torch/autograd/__init__.py", line 251, in backward
            Variable._execution_engine.run_backward(  # Calls into the C++ engine to run the backward pass
        RuntimeError: tensor does not have a device
        ```
