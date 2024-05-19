# 4D $SU(3)$ DEBUG REPORT

```python
>>> trainer = ptExpSU3.trainer
>>> ptExpSU3.trainer.dynamics.init_weights(
...		    method='uniform',
... 			min=-1e-36,
... 			max=1e-36,
... 			bias=True,
... )
>>> beta = torch.tensor(6.0)
>>> zeros = torch.zeros_like(x0)
>>> ones = torch.ones_like(x0)
>>> dynamics = ptExpSU3.trainer.dynamics
>>> config = ptExpSU3.config
>>> g = ptExpSU3.trainer.g
>>> x0_ = ptExpSU3.trainer.g.random(config.dynamics.xshape)
>>> # x0_.shape = torch.Size([1, 4, 2, 2, 2, 2, 3, 3])
>>> avg, diff = g.checkSU(x0_)
>>> print(f'avg: {avg}')
>>> print(f'diff: {diff}')
>>> print(f'x0_.shape: {x0_.shape}')
>>> with autograd.detect_anomaly(check_nan=True):
...     x0_.requires_grad_(True)
...     xout, metrics = trainer.dynamics_engine((x0_, beta))
...     xprop = metrics.pop('mc_states').proposed.x
... 		_xprop = gpt.projectSU(xprop)
... 		loss = trainer.calc_loss(
... 					xinit=x0_,
... 					xprop=xprop,
...			 			acc=metrics['acc']
...			)
... 		# loss.register_hook(
...			#     lambda t: print(f'hook loss = loss:\n {t}')
... 		# )
... 		# loss.register_hook(
...		  #	    lambda t: print(f'hook loss.grad:\n {t.grad}')
... 		# )
...     loss.register_hook(lambda grad: grad.clamp_(max=1.0))
...     trainer.optimizer.zero_grad()
...     print(loss)
...     loss.backward()
...     print(x0_.grad)
...     torch.nn.utils.clip_grad.clip_grad_norm(
...     		trainer.dynamics.parameters(),
...     		max_norm=0.1,
...     )
... 		trainer.optimizer.step()
... 		metrics |= {'loss': loss.item()}
... 		print_dict(metrics, grab=False)
```

```Shell
# [OUTPUT] ------------------------------------------
x0_.shape: torch.Size([4, 4, 1, 1, 1, 1, 3, 3])

avg: tensor[4] f64 x∈[4.240e-07, 5.823e-06] μ=2.579e-06 σ=2.336e-06 grad SqrtBackward0 
[5.823e-06, 1.483e-06, 2.588e-06, 4.240e-07]

diff: tensor[4] f64 x∈[5.743e-07, 1.162e-05] μ=5.051e-06 σ=4.757e-06 grad SqrtBackward0 
[1.162e-05, 2.901e-06, 5.105e-06, 5.743e-07]

tensor f64 grad AddBackward0 -0.031

[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[0.000, 0.470] μ=0.097 σ=0.162
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:259] - [hook] 1/d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:251] - [hook] d:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:252] - [hook] d.grad:
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 all_zeros
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:220] - [hook] torch.acos(rsq3):
 tensor[4, 4, 1, 1, 1, 1] f64 n=16 x∈[-3.155e-29, 2.754e-29] μ=-1.149e-29 σ=1.642e-29
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None
[2023-07-03 13:29:15][INFO][utils.py:225] - [hook] torch.acos(rsq3).grad:
 None

---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
Cell In[97], line 43
     41 trainer.optimizer.zero_grad()
     42 print(loss)
---> 43 loss.backward()
     44 print(x0_.grad)
     45 torch.nn.utils.clip_grad.clip_grad_norm(
     46     trainer.dynamics.parameters(),
     47     max_norm=0.1,
     48 )

File ~/miniconda3/envs/py310/lib/python3.10/site-packages/torch/_tensor.py:491, in Tensor.backward(self, gradient, retain_graph, create_graph, inputs)
    481 if has_torch_function_unary(self):
    482     return handle_torch_function(
    483         Tensor.backward,
    484         (self,),
   (...)
    489         inputs=inputs,
    490     )
--> 491 torch.autograd.backward(
    492 self, gradient, retain_graph, create_graph, inputs=inputs
    493 )

File ~/miniconda3/envs/py310/lib/python3.10/site-packages/torch/autograd/__init__.py:204, in backward(tensors, grad_tensors, retain_graph, create_graph, grad_variables, inputs)
    199     retain_graph = create_graph
    201 # The reason we repeat the same comment below is that
    202 # some Python versions print out the first line of a multi-line function
    203 # calls in the traceback and some print out the last line
--> 204 Variable._execution_engine.run_backward(  # Calls into the C++ engine to run the backward pass
    205 tensors, grad_tensors_, retain_graph, create_graph, inputs,
    206 allow_unreachable=True, accumulate_grad=True)

RuntimeError: Function 'ReciprocalBackward0' returned nan values in its 0th output.
```