---
tags: l2hmc
title: 2022-11-11
date created: Friday, November 19th 2021, 9:38:33 am
---

![l2hmc-qcd|center|300](https://raw.githubusercontent.com/saforem2/l2hmc-qcd/main/assets/logo.svg)


> [!danger]- 📌 Pinned
>  - Paths on ALCF Systems:
>   - Polaris: `/lus/grand/projects/datascience/foremans/polaris/projects/l2hmc-qcd/`
>   - ThetaGPU: `/lus/grand/projects/DLHMC/foremans/l2hmc-qcd/`
> - Install Horovod on MacOS:
> ```bash
> CFLAGS=-mmacosx-version-min=12.5
> HOROVOD_DEBUG=1 
> HOROVOD_WITH_MPI=1
> HOROVOD_WITH_TENSORFLOW=1
> HOROVOD_WITH_PYTORCH=1 
> HOROVOD_WITHOUT_MXNET=1 
> mamba run python3 -m pip install \
>     -vvv --verbose --force-reinstall --no-cache-dir horovod
> ```

> [!todo]- [[001-Areas/work/projects/l2hmc/l2hmc|Task List]]
> ```dataview
> TASK
> FROM "001-Areas/work/projects/l2hmc"
> SORT file.day ASC
> WHERE !completed
> LIMIT 50 
> GROUP BY file.day
> SORT rows.file.day ASC
> ```
>

---


# 2023-07-10

$x \sim \mathcal{N}(0, 1)$
$x' \gets NN(x)$
$min KL(x, x')$


$x \sim p(x)$

$x' \gets x + \alpha_{t} \mathcal{N}(0, 1)$

where $\alpha_{t+1} > \alpha_{t}$ for $t = 0, 1, \ldots$

$\mathcal{L} = KL(p(x'), p(x))$


- 4D $SU(3)$ gradients `NaN` in backward step caused by $\frac{d}{dx} \, \left[acos(x)\right] = \frac{-1}{\sqrt{1 - x^{2}}}$

## `lehner/gpt`
- $SU(n)$ implementation in:
	- [gpt/lib/gpt/core/object_type/su_n.py](https://github.com/lehner/gpt/blob/9e519176439f312034e17b881013d96095ecd9aa/lib/gpt/core/object_type/su_n.py#L130)

- Exp implementation in:
	- [`gpt/lib/gpt/core/matrix/exp.py`](https://github.com/lehner/gpt/blob/9e519176439f312034e17b881013d96095ecd9aa/lib/gpt/core/matrix/exp.py#L121)
 
- Derivative implementation in:
	- [`gpt/lib/gpt/qcd/gauge/action/base.py`](https://github.com/lehner/gpt/blob/9e519176439f312034e17b881013d96095ecd9aa/lib/gpt/qcd/gauge/action/base.py#L23)
 
- [Properties and uses of the Wilson flow in Lattice QCD – Lüscher [2010]](https://link.springer.com/content/pdf/10.1007/JHEP08(2010)071.pdf) 

- [Analytic Smearing of SU(3) Link Variables in Lattice QCD](https://arxiv.org/pdf/hep-lat/0311018.pdf)


> [!abstract]- Papers
> - [On the convergence of dynamic implementations of Hamiltonian Monte Carlo and No U-Turn Samplers](https://arxiv.org/abs/2307.03460)
> - [Augmented Normalizing Flows: Bridging the Gap Between Generative Flows and Latent Variable Models](https://arxiv.org/pdf/2002.07101.pdf)
> - [`lie-nn/sun.py` at main · `lie-nn/lie-nn` · GitHub](https://github.com/lie-nn/lie-nn/blob/main/lie_nn/_src/irreps/sun.py)
> - [Balanced Training of Energy-Based Models with Adaptive Flow Sampling](https://arxiv.org/pdf/2306.00684.pdf)
> - [Generative Modeling through the Semi-dual Formulation of Unbalanced Optimal Transport](https://arxiv.org/pdf/2305.14777.pdf)
> - [Self-Supervised Normalizing Flows for Image Anomaly Detection and Localization](https://openaccess.thecvf.com/content/CVPR2023W/VAND/papers/Chiu_Self-Supervised_Normalizing_Flows_for_Image_Anomaly_Detection_and_Localization_CVPRW_2023_paper.pdf)
> - [Improving Normalizing Flows With the Approximate Mass for Out-of-Distribution Detection](https://openaccess.thecvf.com/content/CVPR2023W/GCV/papers/Chali_Improving_Normalizing_Flows_With_the_Approximate_Mass_for_Out-of-Distribution_Detection_CVPRW_2023_paper.pdf)
> - [Deep Equivariant Hyperspheres](https://arxiv.org/pdf/2305.15613.pdf)
> - [Parameterized Wasserstein Hamiltonian Flow](https://arxiv.org/pdf/2306.00191.pdf)
> - [A General Framework for Equivariant Neural Networks on Reductive Lie Groups](https://arxiv.org/pdf/2306.00091.pdf)
> - [Sampling U(1) gauge theory using a re-trainable conditional flow-based model](https://arxiv.org/pdf/2306.00581.pdf)
> 
> - [Variational Monte Carlo with Large Patched Transformers](https://arxiv.org/pdf/2306.03921.pdf)
> 
> - [Entropy-based Training Methods for Scalable Neural Implicit Sampler](https://arxiv.org/pdf/2306.04952.pdf)
> 
> - [Balanced Training of Energy-Based Models with Adaptive Flow Sampling](https://arxiv.org/pdf/2306.00684.pdf)
> 
> - [Generative Modeling through the Semi-dual Formulation of Unbalanced Optimal Transport](https://arxiv.org/pdf/2305.14777.pdf)
> 
> - [Self-Supervised Normalizing Flows for Image Anomaly Detection and Localization](https://openaccess.thecvf.com/content/CVPR2023W/VAND/papers/Chiu_Self-Supervised_Normalizing_Flows_for_Image_Anomaly_Detection_and_Localization_CVPRW_2023_paper.pdf)
> 
> - [Improving Normalizing Flows With the Approximate Mass for Out-of-Distribution Detection](https://openaccess.thecvf.com/content/CVPR2023W/GCV/papers/Chali_Improving_Normalizing_Flows_With_the_Approximate_Mass_for_Out-of-Distribution_Detection_CVPRW_2023_paper.pdf)
> 
> - [Deep Equivariant Hyperspheres](https://arxiv.org/pdf/2305.15613.pdf)
> 
> - [Parameterized Wasserstein Hamiltonian Flow](https://arxiv.org/pdf/2306.00191.pdf)
> 
> - [A General Framework for Equivariant Neural Networks on Reductive Lie Groups](https://arxiv.org/pdf/2306.00091.pdf)
> 
> - [Sampling U(1) gauge theory using a re-trainable conditional flow-based model](https://arxiv.org/pdf/2306.00581.pdf)
> 
> - [Let us Build Bridges: Understanding and Extending Diffusion Generative Models](https://arxiv.org/pdf/2208.14699.pdf)
> 
> - [MixFlows: principled variational inference via mixed flows](https://openreview.net/pdf?id=HltJfwwfhX)
> 
> - [Semi-supervised learning of order parameter in 2D Ising and XY models using Conditional Variational Autoencoders](https://arxiv.org/pdf/2306.16822.pdf)
> - [Equivariant flow matching](https://arxiv.org/pdf/2306.15030.pdf)
> 
> - [Moving topological charge over the Great Wall in the HMC algorithm - INSPIRE](https://inspirehep.net/literature/880847)
  > > 10.22323/1.091.0026
> 
> - [projUNN/projunn/layers.py at main · facebookresearch/projUNN · GitHub](https://github.com/facebookresearch/projUNN/blob/main/projunn/layers.py)
> 
> 
> - [Gauge-Equivariant Multigrid Neural Networks -- Lehner  & Wettig @ ECT* Trento (ML for Lattice Field Theory + Beyond)](https://indico.ectstar.eu/event/171/contributions/3869/attachments/2471/3408/wettig.pdf)
> 
> - [GLAC/GLAC/math/exponentiation/su3exp.cpp at master · hmvege/GLAC · GitHub](https://github.com/hmvege/GLAC/blob/master/GLAC/math/exponentiation/su3exp.cpp)
> 
> - [GLAC/GLAC/math/exponentiation/su3exp.cpp at 9bb7466fce408bf51cb98d65f639acd37d034d62 · hmvege/GLAC](https://github.com/hmvege/GLAC/blob/9bb7466fce408bf51cb98d65f639acd37d034d62/GLAC/math/exponentiation/su3exp.cpp#L31)
> 
> - [Analytic smearing of SU„3… link variables in lattice QCD _PhysRevD.69.054501_](https://journals.aps.org/prd/pdf/10.1103/PhysRevD.69.054501)
> 
> - [Solving SU(3) Yang-Mills theory on the lattice: a calculation of selected gauge observables with gradient flow](https://s3.cern.ch/inspire-prod-files-0/0969268781511e353ab7cab4a047267f)
> 
> - [Matrix and Tensor Constructions from a Generic SU(n) Vector](https://iopscience.iop.org/article/10.1088/0305-4470/5/7/014/pdf)
> 
> - [pdf](https://iopscience.iop.org/article/10.1088/0305-4470/5/7/014/pdf)
> 



# 2023-05-08
- [ ] Check `Trainer.GradScaler()` object
- [ ] Split up forward / backward methods
- [ ] Prepare submission for PASC23 ; highlight all approaches
- [ ] Submission for Lattice23 @ FNAL ; 2D Scaling Study?[]()
- [ ] Performance w/ volume scaling
- [ ] Deal with Fermions
- [ ] Look @ translation invariance in `s, t, q` functions
- [ ] Look @ sub-volume updates for 2D U(1) model
- [ ] Look @ importance of `s, t, q`, functions
- [ ] Try to understand what `s, t, q` functions are doing in terms of HMC
- [ ] Read through MIT's new paper: [arXiv:2305.02402](https://arxiv.org/abs/2305.02402)


# 2023-03-24
- [ ] Check gradients to make sure things are being updated correctly
- [ ] Compare w/ HMC @ same $\varepsilon$, $\tau$, w/ networks initialized ~ 0.0

# 2023-03-13
- [x] Submitted abstract for PASC23 submission
- [ ] Still working on testing initialization for 4D SU(3) model
- [ ] Ask Ramesh what next steps are / any remaining deadlines

> [!abstract] Generative Modeling and Smarter Sampling for Lattice Gauge Theories
> In this work we describe how recent advancements in generative modeling have contributed to simulations in lattice gauge theory, and discuss some ongoing work in this direction.
>
> In particular, we are interested in generating independent (lattice) configurations, distributed according to the density of our theory. In order to reliably predict values which can be experimentally measured, simulations are carried out at increasing spatial resolution and extrapolated to the continuum (infinite resolution) limit. In this limit, the cost of generating configurations (using existing techniques) is known to scale exponentially, quickly becoming prohibitively expensive, preventing further exploration.
>
> In this work, we present a new technique that uses a generalized version of the Hamiltonian Monte Carlo (HMC) algorithm, parameterized by weights in a neural network, that can be trained to make these simulations more efficient, thereby decreasing the overall computational cost.


# 2023-03-03

- [x] Figure out details of PASC23 submission, submit abstract by (due::03/15/2023)
- [ ] Look closely at weight initialization in 4D SU(3) model
- [ ] Check gradients to make sure things are being updated correctly
- [ ] Compare w/ HMC @ **same** $\varepsilon, \tau$ w/ networks initialized ~ 0.0
- [ ] With networks initialized ~ 0.0, shouldn't be any worse than HMC

# 2023-02-15
- [ ] Ethan Neill Faculty Sabbatical @ ALCF
- [A Tale of Two Latent Flows: Learning Latent Space Normalizing Flow with Short-run Langevin Flow for Approximate Inference](https://arxiv.org/abs/2301.09300)
- [Conditional Normalizing flow for Monte Carlo sampling in lattice scalar field theory arXiv:2207.00980](https://arxiv.org/abs/2207.00980)

## 2023-01-25

- Build out `Timer` object with support for logging to W&B


# 2023-01-13

- Finish testing training methods for 4D SU(3) integrate into `train → eval → analysis` workflow


# 2022-12-09

- Training 4D SU(3) model seems to work in TensorFlow:
```python
>>> from rich import print
>>> from l2hmc.utils.rich import get_console
>>> from l2hmc.network.tensorflow.network import zero_weights
>>> console = get_console()
>>> state_tf = tfExpSU3.trainer.dynamics.random_state(6.0)
>>> xtf = tf.reshape(state_tf.x, tfExpSU3.trainer.dynamics.xshape)
>>> console.log(gtf.checkSU(xtf))
>>> console.log(f'x.shape: {xtf.shape}')
>>> console.log(f'{qcd(xtf).numpy()}')
>>> for epoch in range(50):
        xtf, metrics = tfExpSU3.trainer.train_step_detailed(
            x=xtf,
            epoch=epoch,
            beta=6.0,
            verbose=True,
        )
```

# 2022-11-11
- [ ] Fix momentum update methods for L2HMC w/ 4D SU(3) first, then work on fixing $x$ updates


- Want to scale in $\mathbb{R}$ , shift momentum using TrAH or $\mathfrak{su}(n)$
- 1 real # to scale, 8 to shift
- e^{a}
- Stack `x --> xs = [x.r, x.i] --> NN -->  [scale, [s1, s2, ..., s8]]`




# 2022-11-06
- [x] Merged `dev` into `master` ✅ 2022-11-07
- [x] Updated [experiment.ipynb](https://github.com/saforem2/l2hmc-qcd/blob/main/src/l2hmc/notebooks/experiment.ipynb) ✅ 2022-11-07
- [ ] Write `trainer.burn_in(nchains: int, beta: float) -> Tensor` that runs HMC until $|\delta U_{\mu\nu}| < \varepsilon$ and returns a buffer of `nchains` thermalized configs
- [ ] Write method to reset `train` / `eval` / `hmc` data from `Trainer.histories[...]`

# 2022-10-20
- [[vae-hmc/notes|VAE-HMC Notes]]

# 2022-10-14
- [ ] Look at numerics causing `nan` to appear in training for 4D $SU(3)$ model


# 2022-09-16
## Meeting Notes
`x = [Nb, 4, T, X, Y, Z, 3, 3]`

```python
x0 = x[:, 0, ...]
x1 = x[:, 1, ...]
x2 = x[:, 2, ...]
x3 = x[:, 3, ...]
...
```

# 2022-08-26
## Meeting Notes
- [f] Continue working on 4D SU(3)
- [ ] Try convolutions discussed previously

# 2022-08-19
## Meeting Notes
- `l2hmc` and `fthmc` agree on:
  - `plaqs`
  - `force`
  - `action`
- Need to test / compare:
  - `leapfrog_update`
  - Individual updates
  - Method for `update_gauge`

## 2D $U(1)$
- `x.shape = [Nbatch, 2, nt, nx]`, which is represented as:
  $$x \gets \left[\cos(x), \sin(x)\right]$$
  and has shape `x.shape = [Nbatch, 2, nt, nx, 2]`
- For 2D Convolution, must reshape as 4D Tensor:
  - `xstack = tf.concat([tf.math.cos(x), tf.math.sin(x)])`
    with `xstack.shape = [Nbatch, 4, nt, nx]` ?
- Added `model_improvement` calculation at end of experiment:
  ![[assets/model_improvement.svg|500]]
  - Average over last ~90% and take ratio, write this out to a file.
    - For experiment shown above, `model_improvement = 1876.68859863`

## 4D $SU(3)$
- From `nthmc`:
  ```python
  >>> from l2hmc.nthmc.su3_4d.gauge import SU3d4
  >>> from l2hmc.nthmc.su3_4d import ftr
  >>> action_nthmc = SU3d4(
         tf.random.Generator.from_seed(123),
         1,
         transform=ftr.Ident(),
         beta=0.7796,
         beta0=0.7796,
         c1=0.0,
         size=[8, 8, 8, 16]
     )
  >>> xnt = action_nthmc.random()
  >>> pnt = action_nthmc.randomMom()
  >>> # -------------------------------------------------------
  >>> check_diff(
         action_nthmc.momEnergy(pnt),            # from nthmc
         tfExpSU3.trainer.g.kinetic_energy(pnt)  # from l2hmc
     )
  [08/19/22 08:12:10] INFO     sum(diff): 3.410605131648481e-13                                                    
                               min(diff): 3.410605131648481e-13                                                    
                               max(diff): 3.410605131648481e-13                                                    
                               mean(diff): 3.410605131648481e-13                                                   
                               std(diff): 0.0                                                                      
                               np.allclose: True
  ```





# 2022-08-16
## Meta HMC:
- Learn
  $f: x \rightarrow z$
- HMC:
	- $z' \gets z$
- Loss:
	- $\mathcal{L}_{\theta}(z, z') = \delta(z, z')$
- Inverse:
	- $f^{-1}: z' \rightarrow x'$
- Metropolis Hastings Accept / Reject:
	- $x^{\ast} \gets x'$

# 2022-08-14
- To install horovod on MacOS:

```shell
$ CFLAGS=-mmacosx-version-min=12.5 \
    HOROVOD_DEBUG=1 \
    HOROVOD_WITH_MPI=1 \
    HOROVOD_WITH_TENSORFLOW=1 \
    HOROVOD_WITH_PYTORCH=1 \
    HOROVOD_WITHOUT_MXNET=1 \
    mamba run python3 \
        -m pip install \
        -vvv --verbose \
        --force-reinstall \
        --no-cache-dir \
        horovod
```

# 2022-08-09
- **Naive improvement to annealing schedule**:
	- For $N$ training steps, want to _anneal_ $\beta \in [\beta_{0}, \beta_{N}] = \{\beta_{0}, \beta_{1}, \ldots, \beta_{i}, \ldots, \beta_{N}\}$
	- The graphs below suggest that:
		- `loss` (left plot) continues to improve at start of training ($\beta \simeq \beta_{0}$)
		- `energy` / `logdet` (middle / right  plots) improve drastically at end of training ($\beta \simeq \beta_{1}$)
			- $\Longrightarrow$ Spend _most_ of time training @ beginning and end
			- maybe 25% @ $\beta_{0}$, 25% @ $\beta_{1}$, and 50% in-between?

![[assets/annealing-loss.png|350]] ![[assets/annealing-energy.png|350]] ![[assets/annealing-logdet.png|350]]

# 2022-08-08
- Perform HMC in Latent Space?

$$\begin{align}
z' {\color{red}\gets} z &:= f(x), f: \mathbb{R}^{m}\rightarrow \mathbb{R}^{n}, \,\, m\geq n \\
x^{\ast} {\color{green}\gets} x' &:= f^{-1}(z'), f^{-1}: \mathbb{R}^{n}\rightarrow \mathbb{R}^{m}, \,\, m\geq n \\
\end{align}$$


# 2022-08-05
- ECP-HI Extension Request??
- Fixed PyTorch implementation
- Working on material for ATPESC
	- Organizing ML Day
- Working on debugging $SU(3)$
- Working on debugging Polaris issues
	- Building environment
	- Filesystem issues ??
	- Related to lockfile?
- Trying to run HPO using WandB sweeps
- AI4SS Workshop


# 2022-08-03
- [ ] Create `DataTable` object, inheriting from `rich.table.Table` ?

```python
class DataTable(rich.table.Table):
		def __init__(self, *args, **kwargs):
				super().__init__()
		def add_columns(avgs):
				pass
		def add_row(avgs):
				pass
		def to_file(outfile):
				pass
		...
```

# 2022-07-31
- [ ] Create new objects for:
	- [ ] `BaseTracker(ABC)`
	- [ ] `wandbTracker(BaseTracker)`
	- [ ] `aimTracker(BaseTracker)`
- [ ] Work on creating a database of (non-`debug`) `logdirs`
	- [ ] Start by writing each run dir to a shared file
		- [ ] Create database?
		- [ ] Shared file e.g.

```yaml

path/to/logdir1:
	framework: tensorflow
	name: None
	steps:
		_target_: l2hmc.configs.Steps
		...
	...

path/to/logdir2:
	framework: pytorch
	name: None
	steps:
		_target_: l2hmc.configs.Steps
		...
	...
```

---
# 2022-07-12

- [ ] Add a hook to turn verbose logging on and off
- [ ] Finalize / test + debug `COBALT` job submission scripts
	- [ ] On ThetaGPU
	- [ ] On Polaris
- [ ] Add Jupyter Notebook demonstrating how to aggregate and plot timing data
	- [ ] Send pointer to Sirak by Monday
- [ ] Reach out to twitter / find opportunities

@ $\beta = 6$, $x_{P} \simeq 0.6$

---
# 2022-07-14

- Reviewing INCITE-CR proposals
- Submitted LDRD pre-proposal with researchers from Analytical Chemistry Lab on investigating ML analysis of chemical trace data to detect nefarious substances
- Working on MLPerf HPC submissions
- Working with Romain and Prasanna to build `hydra` integration into `DeepHyper`
- Preparing / reviewing material for DeepHyper Workshop
- Mentoring for GPU Hackathon
- Approved for travel to AI4SS Workshop @ UC-Davis
- Discussion / working with Sirak about implementing scaling studies
	- For the 2D $U(1)$ model, `x.shape = [nchains, 2, nt, nx]`
	- We are interested to see how the model scales with the lattice volume `[nt, nx]` as well as the number of chains

---
# 2022-06-30
- [ ] Theta down for maintenance Mon, Tues
- [ ] Talked to Venkat about ECP-HI extension ✅
	- [ ] Need to send plan to Venkat + James
- [ ] Invited to [AI4SS Workshop](https://ai4ss.lbl.gov/home): **Advanced Research Directions on AI for Science and Security, Workshop Series** @ UC-Davis (July 26-28, 2022)
- [ ] Implement dynamic annealing schedule for $\beta$

## L2HMC
- [ ] Started working on dynamic annealing schedule, initial testing

---
# 2022-06-24
- [ ] Getting Sirak access to `alcf-edge-dev_collab`, `edtb-XX` nodes to run HPO studies on
- [ ] Working on testing / debugging bash scripts for:
	- [ ] Generic (elastic) training
	- [ ] WandB HPO runs
- [ ] Work on getting CELS VM setup for internal WandB deployment
- [ ] Add sirak to WandB slack channel
- [ ] Work on automated annealing schedule where $\beta$ only increased if training is doing "well"
- [ ] Try letting $\lambda$ be trainable parameter?

$$\ell_{\lambda}(x, x') = \frac{\lambda^{2}}{A(x'|x)\cdot \delta(x, x')} - \frac{A(x'|x)\cdot \delta(x, x')}{\lambda^{2}}$$

where e.g. $\delta(x, x') = |Q'_{\mathbb{Z}} - Q_{\mathbb{Z}}|$

---
# 2022-06-17
## Agenda Items
- [ ] LCRC project request wants detailed numbers ???
- [ ] `create_project.py`
- [ ] Diffusion models?
- [ ] Alternative Loss functions
- [ ] Debugging issues with pytorch implementation


## TODO
- [ ] Write job script for running WandB sweeps
- [ ] Talk to Venkat about ECP-HI funding
- [ ] Look at changing $\beta$ continuously
    - [ ] balance against changing learning rate


---
# 2022-06-09
- [ ] Meeting with Sirak James + Xiao-Yong
- [ ] Discussed general ideas about hyperparameter optimization
    - [ ] Try and predict loss curve during training to predict how runs will perform
    - [ ] Might be useful for early stopping criteria?
    - [ ] Keep exploring genetic algorithms
    - [ ] Probably mode useful to run many `wandb.agent`'s in parallel (~2k on Polaris?)
- [ ] Looking at running with

```python
if DynamicsConfig.merge_directions:
    if DynamicsConfig.nleapfrog % 2 == 1:
        DynamicsConfig.nleapfrog *= 2

>>> config = DynamicsConfig(merge_directions=True, nleapfrog=5)
>>> dynamics = Dynamics(config)
>>> dynamics.config.nleapfrog
10
```
```python
if conf.refreshOpt and len(opt.variables())>0:
    tf.print('# reset optimizer')
    for var in opt.variables():
        var.assign(tf.zeros_like(var))
```

- [ ] From run located at:
    - `DLHMC/projects/l2hmc-qcd/src/l2hmc/outputs/runs/U1/16x16/nlf-8/beta-5.0/merge_directions-True/tensorflow/2022-06-09/12-21-53`:

![|350](assets/logdet_ridgeplot.svg) ![|350](assets/logprob_ridgeplot.svg) ![|350](assets/energy_ridgeplot.svg)

$$
\ell(x', x) = \frac{\lambda}{\delta Q^{2}} - \frac{\delta Q^{2}}{\lambda}
$$
where $\lambda = const = 0.01$

---

# 2022-06-03
- Output TAH and

---

# 2022-05-27
- [ ] ECP HI Extension / funding
    - [ ] Reach out to Venkat and get his thoughts
    - [ ] Talk to Chris about funding
- [ ] Want to get 4D SU3 results out by end of summer
- [ ] Check in with Sirak about ALCF accounts
    - [ ] ANL email?
    - [ ] slack access?
    - [ ] ThetaGPU access

## TODO
- [ ] Genetic algorithm approach to increasing $\beta$
- [ ] Push to the limits
- [ ] Figure out what works in 2D $U(1)$
- [ ] Push to the limit
- [ ] Use that information to guide 4D $SU(3)$
- [ ] Work on testing `stop_gradient` implementation and look at:
    - speedup
    - impact on performance?

## Ideas
1. Use VAE to map to latent space
2. HMC in Latent space
3. Map back to physical space
4. Reconstruction loss ?

- [ ] Run HMC in latent space?



---

# 2022-05-20
- [x] [Job talk](https://saforem2.github.io/anl-job-talk) Wednesday
- [x] Working on material for CPW

## TODO
- [ ] reset optimizer at each time $\beta$ changes
- [ ] Run independent trainings with random starts for 5k training steps, find one with best loss, save it, and reload it across all workers and use that as starting point
- [ ] Continue testing speedup for training
- [ ] Test implementation of `stop_gradient` functionality to avoid the calculation of the gradient through[^1] $x_{k}$ in

$$\nabla_{x_{k}} \log p^{\ast}(x_{k})$$

- [ ] Need to better understand / test what effect this has on
    1. Training time / cost improvement
    2. Impact on model performance
    - From [A Gradient Based Strategy for Hamiltonian Monte Carlo Hyperparameter Optimization](https://proceedings.mlr.press/v139/campbell21a.html), they claim that
     > We find this has little impact on convergence and can lead to $5\times$ speedups in execution time



---
# 2022-05-06

## Job Talk

ML & HEP: An Emerging Unexpected Symbiosis

As ML methods continue to grow in popularity and adoption, researchers are beginning to identify new and interesting ways to learn from and interact with their (ever-growing) scientific data. As a result, it is becoming increasingly important for researchers to be able to work effectively with data in order to gain insight and draw meaningful conclusions about their work.

In this talk I will discuss how my research experience in HEP has prepared me to deal with the computational challenges facing scientific workflows on next-generation HPC systems, explain why I think this relationship is mutually beneficial, and offer some ideas for future research directions.
- Working on material for CPW
- [ ] Updated resume and finished application for Venkat
- [ ] Need seminar title and abstract by Today
- [ ] Chatted with Tyler Burch about Normalizing Flows for the Red Sox
- [ ] ANL / W&B sync with Denis, Riccardo, Aditya
- [ ] Helped review AI Testbed documentation and test implementations
- [ ] Working on providing feedback for initial release of HPE Dragon API
- [ ] Added `stop_gradient` functionality to avoid the calculation of the gradient through[^1] $x_{k}$ in $$\nabla_{x_{k}} \log p^{\ast}(x_{k})$$
    - Need to better understand / test what effect this has on:
        1. Training time / cost improvement
        2. Impact on model performance
    - From [A Gradient Based Strategy for Hamiltonian Monte Carlo Hyperparameter Optimization](https://proceedings.mlr.press/v139/campbell21a.html), they claim that
     > We find this has little impact on convergence and can lead to $5\times$ speedups in execution time

## Papers
- [Dimension-independent Markov Chain Monte Carlo on the Sphere](https://arxiv.org/pdf/2112.12185.pdf) #papers
- [Missing Data Imputation and Acquisition with Deep Hierarchical Models and Hamiltonian Monte Carlo](https://arxiv.org/pdf/2202.04599.pdf) #papers
- [Graph Reparameterizations for Enabling 1000+ Monte Carlo Iterations in Bayesian Deep Neural Networks](https://arxiv.org/pdf/2202.09478.pdf) #papers
    - `rir:Github` [JurijsNazarovs/bayesian_nn](https://github.com/JurijsNazarovs/bayesian_nn) #github
- [Exposing the Implicit Energy Networks Behind Masked Language Models via Metropolis-Hastings](https://arxiv.org/pdf/2106.02736.pdf)
    - In this section, we analyze the effectiveness of our proposed MH samplers by evaluating the samples drawn from regions around the mode of the energy functions and evaluating them against references for the task of MT. To achieve this, we propose to perform MH sampling from target distributions whose energy values are scaled by low temperatures i.e. $p(X; \theta T) \propto e^{-\frac{E(X;\theta)}{T}}$ . However, such low-entropy target distributions lead to increased rejection rates for the MH samplers. Therefore, we anneal the temperature as a linear function of epochs to gradually decrease the entropy of the target distribution. In Figure 2 (left, green), we observe that annealing results in dramatic improvements in locally normalized energy scores Enorm, leading to very low energy values. When comparing the acceptance rates, we see that $E_{raw}$ and $E_{norm}$ behave differently as the target distribution temperature is annealed, with the MH samplers under the Eraw target distribution exhibiting larger acceptance rates across the epochs. This difference in acceptance rates also manifests itself in the performance in terms of BLEU scores of the samples under two energy parametrizations, with raw energy parametrization yielding higher BLEU scores.
    - ![[work/projects/l2hmc/assets/screenshot-2022-05-06-083601.png#invert]]
    - Figure 2: Comparison as a function of epochs for the two energy parametrizations (red, blue) for MH approach with annealing toward modes of target energy functions: $E_{raw}$ and $E_{norm}$ on De-En (20). Left: acceptance rates, locally normalized energy (green) as a function of epochs. Right: MT performance. acceptance rates, we see that Eraw and Enorm behave differently as the target distribution temperature


[^1]: https://proceedings.mlr.press/v139/campbell21a.html

---
# [[2022-04-22]]
## Meeting Notes
- [ ] Insert `stop gradient` before calculating force to check
- [ ] Run with and without force gradients
- [ ] Start from $\beta = 4$ @ multiple learning rates, save models (identify best) and use as starting point when increasing $\beta$

### Summer Student
- [ ] Plan to have $SU(3)$ implementation finished, plan for hyperparameter optimization on 4D $SU(3)$ models
- [ ] Implement unit tests
- [ ] Try alternative loss functions
    - [ ] [A Gradient Based Strategy for Hamiltonian Monte Carlo Hyperparameter Optimization](https://proceedings.mlr.press/v139/campbell21a.html)  #papers
    - [ ] [Adaptive Monte Carlo Augmented with Normalizing Flows](https://www.researchgate.net/publication/358976938_Adaptive_Monte_Carlo_augmented_with_normalizing_flows/fulltext/6230c91f069a350c8b8fe83b/Adaptive-Monte-Carlo-augmented-with-normalizing-flows.pdf?_sg%5B0%5D=O_UhGgPPhQkf5250FB2cld6EVSRvViZrWegf81Ty6dFgI7gkScZ41jyl3OPJxoXbcjaBupIc4MBfA1GZD4qVYw._8XcXn5ixnhek5hP1TM4oa5uVQciVLn28Y-VnL07xM7rDpSe8ibARJLVwgpTeAx--8dl_G2-Mql4imUiMlsqnQ&_sg%5B1%5D=tA1InHXHbWEvCGgzAIzUb74vQxX0bk83qysY2TWx_cPDc0x1a_SVKUvmIvYw12gkMiSFBLBQMXkGMgm0eE_8nOnItrTCjbs-Zltg-59wns9O._8XcXn5ixnhek5hP1TM4oa5uVQciVLn28Y-VnL07xM7rDpSe8ibARJLVwgpTeAx--8dl_G2-Mql4imUiMlsqnQ&_sg%5B2%5D=WBLmXc3w1vnqv5OJFBxFPJaBHgtXsA6D6aEXtQHShvkhE9_JV7okhVmyAFqLMq-d7_FqmBEeCB62Cto.cAm4BEuZZilQ5J_b8B0WKZENx1rQqi3aPRIM1G06tbHHIIXateQ7vWWi1ZqqVChawyp0l-TWuqg2nT-T2xY8Zg&_iepl=) #papers
    - [ ] [Transport Score Climbing: Variational Inference Using Forward KL and Adaptive Neural Transport](https://arxiv.org/pdf/2202.01841.pdf)  #papers
        - [ ] [`zhang-liyi/tsc`](https://github.com/zhang-liyi/tsc) [#github](app://obsidian.md/index.html#github)
    - [ ] [Scaling Up Machine Learning For Quantum Field Theory with Equivariant Continuous Flows](https://www.researchgate.net/publication/355110876_Scaling_Up_Machine_Learning_For_Quantum_Field_Theory_with_Equivariant_Continuous_Flows/fulltext/615e9fe5fbd5153f47e9d290/Scaling-Up-Machine-Learning-For-Quantum-Field-Theory-with-Equivariant-Continuous-Flows.pdf?_sg%5B0%5D=96RbxUe7junfQNSOWbQIYiPUSew0D0DaVlZ7RXDAl3WPfQaFW4ejQASrumeIs08Lhmn_S1tJxgy795CJ93DfnA.ux5jwVD9Rfl5r_yuMr36fOmGXALFttW9OdbM7_4U1_z8f-qcoz94JgJ13u0pzi_Vaot9Shm6Va7I1YjZD7p9Ag&_sg%5B1%5D=lltb-Orug3F8NenyKXzqNJMEfiTok4otgYUu31iKoadKZ0DE99I_1gUN55c7ysTAqdd-er5_ATrsvad9ng-NV7yG8udHlNf_kI5tY46VXJr0.ux5jwVD9Rfl5r_yuMr36fOmGXALFttW9OdbM7_4U1_z8f-qcoz94JgJ13u0pzi_Vaot9Shm6Va7I1YjZD7p9Ag&_iepl%5BactivityId%5D=1491178952470538&_iepl%5BactivityTimestamp%5D=1649965970&_iepl%5BactivityType%5D=service_add_recommendation_publication&_iepl%5Bcontexts%5D%5B0%5D=homeFeed&_iepl%5BrecommendationActualVariant%5D=collaborated_referenced_cited_overlap%3Ecollaborated_referenced_cited_overlap&_iepl%5BrecommendationDomain%5D=citations&_iepl%5BrecommendationScore%5D=59.01501083374&_iepl%5BrecommendationTargetActivityCombination%5D=&_iepl%5BrecommendationType%5D=cited_cited&_iepl%5BfeedVisitIdentifier%5D=&_iepl%5BpositionInFeed%5D=1&_iepl%5BsingleItemViewId%5D=UNrtDoq0ANr32a1GeZ0xZl8M&_iepl%5BviewId%5D=0mvTpD1wBoV00JTyAanNj0eD&_iepl%5BhomeFeedVariantCode%5D=ncls&_iepl%5B__typename%5D=HomeFeedTrackingPayload&_iepl%5BinteractionType%5D=publicationDownload&_iepl%5BtargetEntityId%5D=PB%3A355110876)  #papers
    - [ ] [Semi-Discrete Normalizing Flows through Differentiable Tesselation](https://arxiv.org/pdf/2203.06832.pdf)  #papers

### CPW
- [ ] Working on writing material for scaling frameworks
- [ ] Sync w/ Huihuo


## `fthmc`
## Target distribution
$p(U)$ defined on Lie groups $\mathcal{G}$ with $U\in \mathcal{G}$, e.g. $\mathcal{G} = G\otimes G\otimes \cdots \otimes G$ as we have for LGT

## Inputs
1. Prior distribution $r(V)$
2. Invertible flow $f: \mathcal{G}\rightarrow\mathcal{G}$ with tractable Jacobian

## Algorithm
- Generate sample from model by:
    1. sampling from prior distribution $r(V)$
    2. Apply $f$ to produce $U = f(V)$ distributed according to the model density $q(U)$. This can be expressed in terms of the logdet Jacobian of $f$

$$
q(U) = \frac{r(V)}{e^{\sum \log\det|f(V)|}}
$$

where

$$
e^{\sum \log\det|f(V)|} \coloneqq \left|\det_{ij} \frac{\partial \left[f(V)\right]_{i}}{\partial V_{j}}\right|
$$

and the indices $ij$ run over the directions in the Lie algebra of $\mathcal{G}$ translated to $f(V)$ and $V$ respectively.

We can train our model distribution to effectively approximate our target distribution, so that $q(U) \approx p(U)$ by minimizing the KL divergence between the two distributions

$$
D_{\mathrm{KL}}(q \| p):=\int \mathcal{D} U q(U)[\log q(U)-\log p(U)] \geq 0
$$

or, dropping the overall constant $\log Z$,

$$
D_{\mathrm{KL}}^{\prime}(q \| p):=\int \mathcal{D} U q(U)[\log q(U)+S(U)] \geq-\log Z
$$

## `fthmc` $\leftrightarrow$ `l2hmc`
- We can use the trained model density from the `fthmc` approach as the prior distribution for training the `l2hmc` dynamics, i.e

1. Sample $U \sim q(U)$
2. Generate $U'\gets U$ (`leapfrog layer`)
3. Evaluate `l2hmc` loss, $\mathcal{L}_{\theta}$

We can write a generic loss function $\mathcal{L}_{\theta}$ as a sum of distinct terms (e.g. plaquette, topological charge, etc.)

$$
\ell_{k}(U', U) = \alpha_{k}\cdot \delta_{k}(U', U)
$$

where $\alpha_{k}\in\mathbb{R}$ are tunable weights that allow us to control individual terms' relative contribution to the total loss.

We can then express the total loss as an expectation value over a weighted sum of these terms, making explicit note of the fact that $U \sim q(\cdot)$

$$
\mathcal{L}_{\theta} = \mathbb{E}_{q(U)}\left[\sum_{k} \ell_{k}(U', U)\right]
$$

We can consider additional contributions to our loss at each training step by drawing an _additional_ batch of samples $W \sim \pi(\cdot)$, which are then passed through the `l2hmc` dynamics to generate a proposal configuration $W'\gets W$.

In this case, the complete loss function is then


$$
\mathcal{L}_{\theta} = \mathbb{E}_{q(U)}\left[\sum_{i}\alpha^{i}\ell_{i}(U', U)\right] + \mathbb{E}_{\pi(W)}\left[\sum_{i}\alpha^{i}\ell_{i}(W', W)\right]
$$

## Equivariant Manifold Flows
- A Riemannian manifold $(\mathcal{M}, h)$ is an $n$-dimensional manifold with a smooth collection of inner products $(h_x)_{x\in\mathcal{M}}$ for every tangent space $T_{x}\mathcal{M}$. The Riemannian metric $h$ induces a distance $d_h$ on the manifold
- A diffeomorphism $f: \mathcal{M}\rightarrow\mathcal{M}$ is a differentiable bijection with differentiable inverse.
- A Diffeomorphism $f: \mathcal{M}\rightarrow\mathcal{M}$ is called an <mark style="background: #FFFF00A6;">isometry</mark> if $h(D_{x}f(u), D_{x}f(v)) = h(u, v)$ for all tangent vectors $u, v \in T_{x}\mathcal{M}$ , where $D_{x} f$ is the differential of $f$
    - Note that isometries preserve the manifold distance function
    - The collection of all isometries forms a group $G$, called the _isometry group_ of $\mathcal{M}$
- **Riemannian gradient**: Define the riemannian gradient $\nabla_{x} f$ to be the vector on $T_{x}\mathcal{M}$ such that $h(\nabla_{x} f, v) = D_{x} f(v)$ for $v \in T_{x}\mathcal{M}$

## Normalizing Flows on Manifolds
### Manifold Normalizing Flow
- Let $(\mathcal{M}, h)$ be a Riemannian manifold. A normalizing flow on $\mathcal{M}$ is a diffeomorphism $f_{\theta}:\mathcal{M}\rightarrow\mathcal{M}$ (parameterized by $\theta$) that transforms a prior density $r$ (a.k.a $\rho$) to a model density $q$ ( a.k.a $\rho_{f_{\theta}}$)
- The model distribuion can be computed tvia the Riemannian change of variables:

$$
q(x) = r\left(f^{-1}_{\theta}(x)\right) \left|\det_{h} D_{x} f^{-1}_{\theta}\right|
$$

### Manifold Continuous Normalizing Flow
- A manifold continuous normalizing flow with base point $z$ is a function $\gamma: [0, \inf)\rightarrow \mathcal{M}$ that satisfies the manifold ODE

$$
\frac{d \gamma(t)}{dt} = X(\gamma(t), t), \quad \gamma(0) = z
$$

- We define $F_{X, T}: \mathcal{M}\rightarrow\mathcal{M}$, $z \mapsto F_{X, T}(z)$ to map any base point $z \in \mathcal{M}$ to the value of the CNF starting at $z$, evaluated at time $T$
- Here $\gamma(t)$ is referred to as the (**vector field**) **flow** of $X$






---
# [[2022-04-15]]

See how optimal learning rate varies with $\beta$

- [x] Working on "speeding up" training for $32\times32$ lattice at $\beta = 5$
- [x] Started [`wandb.sweep`](https://wandb.ai/l2hmc-qcd/l2hmc-qcd/sweeps/7hzl03o6?workspace=user-saforem2) over `learning_rate.lr_init` values


![[PeriodicNotes/Daily/assets/32x32-beta5-lr_init.svg#invert|500]]

![[PeriodicNotes/Daily/assets/32x32-beta5-lr_init-dQint-train-avg.svg#invert|500]]

![[PeriodicNotes/Daily/assets/32x32-beta5-lr_init-dQint-eval-avg.svg#invert|500]]

![[PeriodicNotes/Daily/assets/32x32-beta5-lr_init-dQint-hmc-avg.svg#invert|500]]


---
# [[2022-04-07]]

$$
S_{g}= - \frac{\beta}{3}\left[(1 - 8 \,c_{1} )\sum_{x,\nu<\mu} P_{\mu\nu}(x) + c_{1}\sum_{x, \mu\neq\nu} R_{\mu\nu}(x)\right]
$$

$$
Q = \frac{1}{32\pi^{2}}\sum_{\mathbf{x}, t} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left[\hat{F}_{\mu\nu}(\mathbf{x}, t)\hat{F}_{\rho\lambda}(\mathbf{x}, t)\right]
$$

where $\hat{F}_{\mu\nu}(x; m, n) =$

![[Excalidraw/field-strength.svg|400#invert]]

- [x] Try simple network and change Adam parameters
- [x] Try and speedup training
    - [x] See if its possible?
- [ ] Scale up $\beta$

---
# [[2022-04-01]]
- [x] Try simplest network possible
- [x] $\beta = 4$ on $32\times 32$ lattice with very simple network
- [x] Try and see what the best we can get in training performance
- [x] Run for some number of steps (50k)
    - Try different network sizes and type
    - Try tuning optimizer parameters to see what is best at end of training

---

# [[2022-03-25]]
- [x] Reset optimizer state each time $\beta$ changes #important
TRIM_WHITESPACE_REPLACE_1


## Done
- [x] [Physics Seminar Talk](https://saforem2.github.io/physicsSeminar/#/)
- [x] Setup environment on `edtb-02` with #tensorflow  #pytorch #horovod and #cuda
- [x] Setup interviews with potential summer research student candidates

## L2HMC
Denote by $M^{\pm} = \left(\begin{smallmatrix}\Gamma^{\pm} & \cdot \\ \cdot & \Lambda^{\pm}\end{smallmatrix}\right)$, with $\xi = \left(\begin{smallmatrix} v\\ x \end{smallmatrix}\right)$ we have that $$\xi^{\pm} = M^{\pm}\xi \Longrightarrow \xi = M^{\mp}\xi^{\pm}$$

## [Adversarially Training MCMC with Non-Volume Preserving Flows](https://mdpi-res.com/d_attachment/entropy/entropy-24-00415/article_deploy/entropy-24-00415-v2.pdf)
### Using Non-Volume Preserving Flows as Generator
We construct three layers of the non-volume-preserving flow model as the generator. We firstly update the auxiliary momentum variables via

$$
v' = v + \varepsilon\, T(x)
$$

where $T(x)$ is a translation item determined by $x$.

> [!question] Don't scale $v$?
> We do not multiply a scale item to $v$ like RNVP, because we find that it can bring much worse results and is difficult to train


Next we update $x$ through the transition function:

$$
x' = x\odot \exp\left[\varepsilon S(v')\right] + T(v') \odot \exp\left[\varepsilon S(v')\right]
$$

where $S(v')$ is the scale item and $T(v')$ is the translation item that is determined by $v'$.

> [!NOTE] Single $x$ update
> We note that our transition kernels update $x$ in a single step (as opposed to updating complementary components in steps). When a part of $x$ is updated through another part of $x$, trhe correlation between data will inevitably increase. Thus, we gave up this approach and only updated $x$ based on $v$

At each epoch of training, we generate samples through the transition kernels and use the MH algorithm to compute acceptance probability. We treat all the samples from the transition kernels as the “fake samples”, and treat the samples from the buffer as the “true samples”. ==A discriminator will be trained to distinguish the “true samples” from the “fake samples”. Our transition kernel will be trained to fool the discriminator==. After getting new samples, we drop some samples of the buffer in a constant ratio and insert the new accepted samples, and thereby the quality of samples in the buffer can be improved. We train our parameters in the framework of GANs, and the training objective can be formulated as:

$$
\min_{K} \max_{D} V(D, K) = \min_{T} \max_{D} \mathbb{E}_{x\sim B(x)}\left[D(x) \right] - \mathbb{E}_{z\sim\mathcal{N}(0, 1)}\left[D(K(z))\right]
$$


---

# [[2022-03-11]]
## Todo
- [ ] Find best HMC step size for each and find the best we can do for each beta and compare
- [ ] Start with best set of parameters from 16 as starting point for 32 volume
- [ ] Do more careful evaluation of parameter space

## Summer Student Project
Title: **Hyper-Parameter Optimization and Scaling Studies of ML Models in Lattice Field Theory**
Description:

- **Hyperparameter Optimization and Scaling Studies of ML Models in Lattice Field Theory**
> Recently there has been notable progress towards using ML as a general tool to make large-scale simulations more computationally efficient. While promising, we can anticipate a variety of issues and challenges which will need to be overcome in order to scale these methods up to more complicated theories on larger lattice volumes. One important goal of the proposed research would be to develop a better understanding of how different hyperparameter configurations ultimately impact model performance and training cost, and to identify an “optimal” set of hyperparameter configurations that can help provide guidance for future experiments. An equally important direction would be to perform a detailed scaling study of how the training cost and expected performance of these simulations scales with lattice volume and network size.

- Recently, there has been notable progress towards using ML as a general tool to make large-scale simulations more computationally efficient.
- While promising, we can anticipate a variety of issues and challenges which will need to be overcome in order to scale these methods up to more complicated theories on larger lattice volumes.
- One important goal would be to develop a better understanding of how different hyperparameters ultimately impact model cost and performance, in addition to identifying an “optimal” set of hyperparameter configurations that can help provide guidance for future experiments.
- Another important research direction would be to perform a detailed scaling study of how the training cost and expected performance improvement of our approach scales with lattice volume and network size.

    1. Model performance scales with lattice volume and network size
    2. Training cost scales with lattice volume and network size
        1. Should we expect the complexity of the network to have to scale with lattice volume?
        2. Can we overcome this with clever architectures?
        3. Do we expect network size to have to scale with volume?
        4. How can we optimize / simplify?

    - There are two directions:
        1. Scaling network size
            - Expect to have to scale network size (sizes of hidden layers) with lattice volume?
            - Can we fix with ConvNets? Gauge Equivariant Conv Nets? GNNs??
        2. Scaling Lattice Volume

## W&B Reports
- [$32\times32$](https://wandb.ai/l2hmc-qcd/l2hmc-qcd/reports/Quality-Checks-32-x-32---VmlldzoxNjc1MjU4)
- [$64\times64$](https://wandb.ai/l2hmc-qcd/l2hmc-qcd/reports/Quality-Checks-64-x-64--VmlldzoxNjc1MTE3)

## Paper
- [ ] [Mitigating the Hubbard Sign Problem with Complex-Valued Neural Networks](https://arxiv.org/pdf/2203.00390.pdf) #papers #toRead

---

# [[2022-03-04]]

- [ ] Look at removing $s(\xi)$ from $x$ update function #work #l2hmc
- [ ] Look at removing forward / backward updates  #work #l2hmc
- [ ] Scale up volume $16\longrightarrow 32 \longrightarrow 64$ #work #l2hmc

---

# [[2022-02-25]]
- [ ] [Semi-Equivariant GNN Architectures for Jet Tagging](https://arxiv.org/abs/2202.06941) #papers
    - [ ] **Ant factor**: Metric that compares the classification power of a model (i.e. how much weight it can lift) with a model's size. This measure allows us to prioritize a subset of resource-efficient HP configurations.
- [ ] [Flow-based sampling in the lattice Schwinger model at criticality](https://arxiv.org/abs/2202.11712) #papers

## Todo
- [ ] Finish running + checking tests for:
    - [ ] `dynamics.merge_directions = [True, False]`
    - [ ] `net_weights.x.s = [0, 1]`
- [ ] Work on quantizing model improvement as a function of network sizes
     - [ ] Find minimal network sizes to obtain acceptable results
- [ ] Implement unittests for `Dynamics` `Trainer`, etc.
- [ ] Update #tensorflow `Trainer` to mimic HMC changes in #pytorch `Trainer`
- [ ] Figure out #horovod issues when training on multiple GPUs with TensorFlow
- [ ] Test / compare `ConvNet` architectures to strictly `Dense` layers
- [ ] Try generalizing / allowing for distinct architectures for $s_{k}$, $t_{k}$, $q_{k}$, $k \in x, v$
- [ ] Figure out low acceptance rate issue for #hmc

![hmc|invert](work/projects/l2hmc/assets/Pasted%20image%2020220225084954.png)

## Completed
- [x] Reverse momentum explicitly ✅ 2022-02-25
- [x] Perform all forward steps ✅ 2022-02-25
- [x] Added support for tracking lattice metrics ($x_{P}$, $Q_{\mathbb{Z}}$, $Q_{\mathbb{R}}$, $\delta Q_{\mathcal{X}}$) during both training and evaluation #l2hmc
- [x] Finished organizing metrics in W&B Dashboard
- [x] Consistent naming of metrics across #pytorch and #tensorflow implementations

---

# [2022-02-18](PeriodicNotes/Daily/2022-02-18.md)
- [ ] Finish backend / metric tracking / experiment management with W&B + TensorBoard
- [ ] Automatic grouping / improvement analysis / historic tracking

## Completed
- [x] Added distributed training support (`horovod` and `DDP`) for #tensorflow and #pytorch in #l2hmc
- [x] Added experiment management and metric tracking support for TensorBoard and W&B #l2hmc

---

# 2022-02-11
- [ ] Try running `net_weights` tests to determine importance of $s_{x}$, $s_v$ terms  #l2hmc #work
- [ ] Look at scaling tests, try to determine smallest networks that are capable of improving performance #l2hmc #work
- [ ] Try generalizing by allowing each of the $s, t, q$ networks to be independent with different architectures ? #l2hmc #work
- [ ] Explain situation about reproduced figure for PANDAS approval #work

---

# 2022-02-04
- [x] Reverse momentum explicitly
- [x] Perform all forward steps
- [x] Reverse momentum
- [x] Perform all backward steps

---

# 2022-01-21
- [x] Talk about summer students ?
- [x] Mention Dragon / Venkat's request for a lead [brief documentation](https://www.hpe.com/psnow/doc/4aa6-5780enw)

## Meeting Notes
- [ ] Wont be able to be on Rapids
- [ ] Keep separate on ASCR
- [ ] Fix size of hidden layers and look at scaling
- [ ] Fixed batch size, increase volume, look at scaling
- [ ] Does total training time decrease as we increase total number of GPUs?
- [ ] $32\times32$ suppose 1 copy / gpu
- [x] TEST FORWARD BACKWRD #important
    - Instead of restricting `DynamicsConfig.nleapfrog % 2 == 0`, if `DynamicsConfig.merge_directions` then `DynamicsConfig.nleapfrog *= 2`
 TRIM_WHITESPACE_REPLACE_1

---

# 2022-01-14

## To Discuss
- [ ] Updates to `l2hmc`,
    - [ ] Re-organized directory / module structure
    - [ ] Re-wrote `Dynamics` objects to use unified `config` objects
    - [ ] Plan to incorporate [Hydra](https://hydra.cc/docs/patterns/select_multiple_configs_from_config_group/) for experiment management
- [ ] How to make reversible without explicit forward / backward updates?
- [ ] Look again at net weight scaling and impact on performance
    - [ ] Determine if all three functions $S$, $T$, and $Q$ are necessary and important for model performance
- [ ] Relation between #l2hmc and #fthmc

## Done
- [x] Submitted application to [[DSECOP Fellowship Application]]
- [x] Sent OAR Postdoc Summary

## Todo
- [ ] Update LeapfrogLayers preprint on arXiv
- [x] Update #l2hmc section in [SciDAC-5 proposal](https://www.overleaf.com/project/61d721f2931495ed8d67af03) #important ✅ 2022-09-16
    - [ ] Update summary with #l2hmc
    - [ ] Keep brief and include maybe a few (2) plots demonstrating results
    - [ ] Give overview of method / network approach
- [ ] Brainstorm ideas for connections with Prasanna for connections with DeepHyper
- [ ] Symmetry preserving network architectures
- [ ] Demonstrate example of

---

# 2022-01-06
## l2hmc $\longleftrightarrow$ fthmc
### Training Step
### l2hmc
- input: $x$
- **Algorithm**:
    1. Generate proposal configuration $x'$ by passing $x$ through the L2HMC dynamics
    2. Calculate acceptance probability $A(x'|x)$
    3. Evaluate loss $\mathcal{L}_{\theta}(x, x') = \sum_{\alpha} \alpha\cdot A(x'|x) \cdot \ell_{\alpha}(x, x')$
    4. Back-propagate gradients and update network weights $\theta$
    5. Perform Metropolis-Hastings accept/reject step and return $x^{\ast} = A(x'|x)\cdot x'$


## Meeting notes
- [ ] Elaborate on recent `l2hmc-qcd` updates from `src` branch slack
- [ ] Look again at net weight scaling and impact on performance
- [ ] Ask about ML models for HEP more generically, model selection observable prediction uncertainty analysis
- [ ] Add reference to [arXiv:2106.14234](https://arxiv.org/pdf/2106.14234.pdf)
- [ ] Add sentence making clear that we're not really interested in 2D, using HMC as baseline to compare with other methods
    - [ ] Not considering these here, ultimate goal is to scale to full QCD
    - [ ] Mention that there exist better methods than HMC
    - [ ] Only cite Eichhorn, mention that these methods don't scale to full QCD
- [ ] Move Eichhorn reference to introduction
- [ ] Common base model U(1) used as toy case for HMC

## SciDAC-5 Proposal
- [ ] organize into related ideas
    - [ ] ideas for model architecture
    - [ ] training
    - [ ] infrastructure
    - [ ] scaling up
    - [ ] connections to rapids
- [ ] refine / develop cohesive idea about GNNs
    - [ ] identify relevant connections
- [ ] Expand upon connections,
- [ ] Find most recent experiments that look at scaling the functions

---

# 2021-01-01
## SciDAC-5 Proposal
- [ ] Well developed libraries for model parallelism
- [ ] Low-rank approximations of dense layers
- [ ] Gauge + Rotation equivariant architectures
- [ ] graph neural networks ?
- [ ] [geometric deep learning](https://geometricdeeplearning.com/)

## Road map
- [ ] Try incorporating $SU(3)$ gauge model in 2 and 4D

---

# 2021-12-10
- [ ] Main theme of SciDAC proposal: **multi-scale algorithms** #work
- [ ] Want code to be **very** flexible
- [ ] Try plugging things into #python
    - [ ] As things move on, eventually remove #python ? replace with #nim
- [ ] Proposed research plan:
    - [ ] hammer-out details of what would need to be done
    - [ ] Ideally (would need to) engage with CS side _somehow?_
    - [ ] [gpt](https://github.com/lehner/gpt)
- [ ] Solver-side:
    - [ ] postdoc in fast-math
    - [ ] planning on working with petsc
    - [ ] ANL will most likely hire postdoc to work with fast-math + petsc
- [ ] email Prassana first saying we saw these people in rapids we plan to talk to
    - [ ] Sandeep Madireddy
    - [ ] Romit Maulik
        - [ ] putting together scidac
        - [ ] looking to interface with things
        - [ ] get his ideas about some things
        - [ ] don't promise anything but mention that we're working on it, gauge interest
- [ ] Experiment with model parallelism in existing code
- [ ] Experiment with interfacing with existing lattice code
- [ ] Worth referencing LBANN, [deepspeed](https://www.deepspeed.ai)
- [ ] Work on reproducing #fthmc #l2hmc with model-parallelism
- [ ] Try trunning very large lattice with model parallelism by hand,
    - [ ] better understand limitations of training libraries (horovod, deepspeed, etc.)
- [ ] [Equivariant Maps for Hierarchical Structures](https://arxiv.org/pdf/2006.03627.pdf)
- [ ] Is sampling in pure gauge solved for large $\beta$? #work
- [ ] Implement over-relaxed heatbath #work
- [ ] Need fermions #l2hmc #work
- [ ] Compare #fthmc vs #l2hmcA (as much as we can) #work
- [ ] If `acc == 0` during training, redraw $x\sim\mathcal{U}(\pm\pi]$
- [ ] Build new environment with updated conda and Nvidia drivers #python #work
- [x] Finishing slides for talk "DWQ@25" Workshop @ BNL (@[[2021-12-13]]) #important #work ✅ 2021-12-20
- [ ] Aurora Workshop #work
- [ ] Follow #tensorflow [transformer doc](https://www.tensorflow.org/text/tutorials/nmt_with_attention) for re-writing  #work

---

# 2021-12-03
- [ ] Ask Denis about plans for scaling up to 4D, dealing with fermions, model parallelism  #work
- [ ] <mark class="blue">Efficient Markov Chain Monte Carlo Sampling Techniques</mark>
    - [ ] Project to be included on [AI Web Site](https://www.anl.gov/ai)  #work
     - [ ] Fill out template by
- [x] Interview with Laura, sent email to media@alcf.anl.gov to give heads up #work
    - [x] Put Laura in contact with Beth Cerny #work
- [x] Complete [ALCF Survey](https://cvent.me/DX8KxG) by ⏰ 2021-12-31 📅 2021-12-31 #work [completion:: 2022-07-16]
- [ ] Look at [Fermilab Fellowships](https://fnal.gov/pub/forphysicists/fellowships/index.html) #work #life #jobs
- [x] Look at [Peoples Fellowship](https://academicprogramsonline.org/ajo/fellowship/20502) @ Fermilab due by 📅 2022-02-12 #work #life #jobs [completion:: 2022-07-16]
- [x] Present work at Aurora Workshop Part 2, **December 7-9, 2021** ??

## l2hmc
 - [ ] [google/ml_collections](https://github.com/google/ml_collections) for `ConfigDict` objects #work
 - [ ] Implement learning rate warm up for #fthmc
     - [ ] mimic #fthmc directory structure for #l2hmc
 - [ ] Split up training into era / epoch format for #l2hmc

## SnowMass

- [ ] Discussion on **community tools and standards in ML** whitepaper #snowmass
- [ ] Work on [Snowmass ML for Lattice White Paper](https://www.overleaf.com/project/61940ef029eb341a502e371c) #snowmass
- [ ] Reply to Savannah about GNN WhitePaper for #snowmass
    - [ ] Graph transformers
    - [ ] Normalizing Flows on graphs
    - [ ] [geometricdeeplearning](https://www.geometricdeeplearning.com)

---

# 2021-11-29

- [ ] Ask #DataScience group about model parallelism #work
- [ ] Work on getting pytorch implementations compatible with DDP #work
- [x] Re-purpose [ML+NN 4 LFT](https://www.snowmass21.org/docs/files/summaries/CompF/SNOWMASS21-CompF3_CompF2_Sam_Foreman_(V2)-131.pdf) for AI@DOE White Paper 📅 2021-11-30 #work
- [x] <mark class="pink">Submit lattice proceedings!</mark> 📅 2021-11-30 #l2hmc #fthmc
- [ ] HEP SciDAC
- [x] Motivate problem in #fthmc proceeding and describe charge freezing
    - [x] Include diagram ?
 - [ ] Explicitly indicate that $x$ is multivariate in #fthmc
 - [x] Include training details, hyperparameters, etc
 - [x] Include equation explaining ESS
 - [x] Describe training time, mention cheapness
 - [x] email media@alcf.anl.gov to let them know and give a heads up about interview
 - [x] Include ALCF blurb in both proceedings' acknowledgments sections


## NeurIPS 2021
- [ ] **Lattice Gauge Symmetry in Neural Networks** [arXiv:2111.04389](https://arxiv.org/pdf/2111.04389.pdf)
  - [ ] `ris:Github` [openpixi/lge-cnn](https://gitlab.com/openpixi/lge-cnn)
    - `ris:GitBranch` [dmueller/lge-cnn/new_modules](https://gitlab.com/dmueller/lge-cnn/-/tree/new_modules)
    - `ris:GitBranch` [schuh93/lge-cnn/baselines](https://gitlab.com/schuh93/lge-cnn/-/tree/baselines)
- [ ] [Entropy-based adaptive Hamiltonian Monte Carlo](https://proceedings.neurips.cc/paper/2021/hash/ef82567365bc6a0efb05d21837257424-Abstract.html)  #papers #toRead #l2hmc
  - [ ] `ris:Github` <a href="https://github.com/marcelah/entropy_adaptive_hmc">entropy_adaptive_hmc</a>
- [ ] [E(n) Equivariant Normalizing Flows](https://proceedings.neurips.cc/paper/2021/hash/21b5680d80f75a616096f2e791affac6-Abstract.html)
- [ ] [Vector-valued GPs on Riemannian Manifolds via Gauge Independent Projected Kernels](https://proceedings.neurips.cc/paper/2021/hash/8e7991af8afa942dc572950e01177da5-Abstract.html)
- [ ] [Gauge Equivariant Transformer](https://proceedings.neurips.cc/paper/2021/hash/e57c6b956a6521b28495f2886ca0977a-Abstract.html) #papers #toRead
- [ ] [Group Equivariant Subsampling](https://proceedings.neurips.cc/paper/2021/hash/2ea6241cf767c279cf1e80a790df1885-Abstract.html) #papers
  - [ ] `ris:Github` [jinxu06/gsubsampling](https://github.com/jinxu06/gsubsampling) #papers #toRead
- [ ] [Equivariant Manifold Flows](https://proceedings.neurips.cc/paper/2021/hash/581b41df0cd50ace849e061ef74827fc-Abstract.html) #papers #toRead
- [ ] [Self-Interpretable Model with Transformation Equivariant Interpretation](https://proceedings.neurips.cc/paper/2021/hash/1387a00f03b4b423e63127b08c261bdc-Abstract.html) #papers #toRead

---

# 2021-11-20
## l2hmc
- [ ] Finish Lattice proceedings
- [x] Plot $N_{\mathrm{LF}}\cdot \tau_{\mathrm{int}}$ vs $N_{\mathrm{LF}}$ with multiple $x$-axes ✅ 2021-12-03
- [ ] Try NN with explicit directional symmetry to avoid having to use forward / backward updates