---
cssclasses:
  - img-max
title: meeting-notes
project: FTHMC, lattice-qcd, MCMC
tags:
  - fthmc
  - "#lattice"
  - "#MCMC"
  - meeting-notes
---
# Field Transformation & Trivializing Maps

## 2023-10-16

- [Diffusion Models as Stochastic Quantization in Lattice Field Theory](https://arxiv.org/abs/2309.17082)
    - [obsidian link](paper-discussion/Diffusion%20Models%20for%20LQCD/Diffusion%20Models%20as%20Stochastic%20Quantization%20in%20Lattice%20Field%20Theory.md)
    
- [Diffusion Generative Flow Samplers: Improving Learning Signals Through Partial Trajectory Optimization](https://arxiv.org/abs/2310.02679)
- [Neural Sampling in Hierarchical Exponential-family Energy-based Models](https://arxiv.org/abs/2310.08431)
- [Neural Diffusion Models](https://arxiv.org/abs/2310.08337)
- [Lattice real-time simulations with learned optimal kernels](https://arxiv.org/abs/2310.08053)
- [Deterministic Langevin Unconstrained Optimization with Normalizing Flows](https://arxiv.org/abs/2310.00745)
- [Entropy-MCMC: Sampling from Flat Basins with Ease](https://arxiv.org/abs/2310.05401)
- [Deterministic Langevin Unconstrained Optimization with Normalizing Flows](https://arxiv.org/abs/2310.00745)


## 2023-07-03
> [!tldr]+ References
> - [Variational Monte Carlo with Large Patched Transformers](https://arxiv.org/pdf/2306.03921.pdf)
> - [Entropy-based Training Methods for Scalable Neural Implicit Sampler](https://arxiv.org/pdf/2306.04952.pdf)
> - [Balanced Training of Energy-Based Models with Adaptive Flow Sampling](https://arxiv.org/pdf/2306.00684.pdf)
> - [Generative Modeling through the Semi-dual Formulation of Unbalanced Optimal Transport](https://arxiv.org/pdf/2305.14777.pdf)
> - [Self-Supervised Normalizing Flows for Image Anomaly Detection and Localization](https://openaccess.thecvf.com/content/CVPR2023W/VAND/papers/Chiu_Self-Supervised_Normalizing_Flows_for_Image_Anomaly_Detection_and_Localization_CVPRW_2023_paper.pdf)
> - [Improving Normalizing Flows With the Approximate Mass for Out-of-Distribution Detection](https://openaccess.thecvf.com/content/CVPR2023W/GCV/papers/Chali_Improving_Normalizing_Flows_With_the_Approximate_Mass_for_Out-of-Distribution_Detection_CVPRW_2023_paper.pdf)
> - [Deep Equivariant Hyperspheres](https://arxiv.org/pdf/2305.15613.pdf)
> - [Parameterized Wasserstein Hamiltonian Flow](https://arxiv.org/pdf/2306.00191.pdf)
> - [A General Framework for Equivariant Neural Networks on Reductive Lie Groups](https://arxiv.org/pdf/2306.00091.pdf)
> - [Sampling U(1) gauge theory using a re-trainable conditional flow-based model](https://arxiv.org/pdf/2306.00581.pdf)
> - [Let us Build Bridges: Understanding and Extending Diffusion Generative Models](https://arxiv.org/pdf/2208.14699.pdf)
> - [MixFlows: principled variational inference via mixed flows](https://openreview.net/pdf?id=HltJfwwfhX)
> - [Semi-supervised learning of order parameter in 2D Ising and XY models using Conditional Variational Autoencoders](https://arxiv.org/pdf/2306.16822.pdf)
> - [Equivariant flow matching](https://arxiv.org/pdf/2306.15030.pdf)
> 
## 2023-03-06

- [ ] XYJ Updates about Training Progress

- [ ] `fthmc` for 4D SU(3) model ??


- Papers to discuss:
	1. Conditional Normalizing Flow for Markov Chain Monte Carlo sampling in the critical region of lattice field theory [Phys. Rev. D 107, 014512](https://journals.aps.org/prd/abstract/10.1103/PhysRevD.107.014512)
	2. Reduction of Autocorrelation Times in Lattice Path Integral Quantum Monte Carlo via Direct Sampling of the Truncated Exponential Distribution [arXiv:2302.04240v1](https://arxiv.org/abs/2302.04240)
	3. Transport Map Unadjusted Langevin Algorithms [arXiv:2302.07227](https://arxiv.org/abs/2302.07227)
	4. Timewarp: Transferable Acceleration of Molecular Dynamics by Learning Time-Coarsened Dynamics [arXiv:2302.01170](https://arxiv.org/abs/2302.01170)
	5. Towards the Application of Skewed Detailed Balance in Lattice Gauge Theories [doi:10.22323/1.430.0028](https://inspirehep.net/literature/2634470)
	6. A Tale of Two Latent Flows: Learning Latent Space Normalizing Flow with Short-run Langevin Flow for Approximate Inference [arXiv:2301.09300](https://arxiv.org/abs/2301.09300)

In addition / alternatively, if people are interested, I can give some updates about the L2HMC work.

# 2022-08-22
## L2HMC
- [x] HMC for 4D $SU(3)$ working

![[assets/plaqs-SU3d4-tf.png]]

![[assets/plaqs-SU3d4-pt.svg]]

- [ ] `su3_to_vec` is in the algebra
- [ ] If we turn off `xnet` it should work as is for the Force and momentum
- [ ] Use 3D Convolutions for 4D input
  - [ ] `su3_to_vec`: [Nbatch, 4, nt, nx, ny, nz, 3, 3] --> [Nbatch, 4, nt, nx, ny, nz, 8]
  - [ ] Shift in `nt` direction by `kernel_size`
  - [ ] Call 3D Convolution on `nx, ny, nz`
  - [ ] For kernel size `k`
  - [ ] [Nbatch, 4, nt, nx, ny, nz, 3, 3] --> [Nbatch * 4 * nt, nx, ny, nz, k * 8]
  - [ ] Call 3D Convolution on [Nbatch * 4 * nt, nx, ny, nz, k * 8]







