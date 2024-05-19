---
created: 2022-03-07 12:27:58
---
# ASCR Highlight Slide L2HMC (2022)

![[assets/leapfrog_layers.pdf]]

![autocorr|500](assets/autocorr.png)

## Scientific Achievement
- We develop a trainable framework that can be used to speed up existing sampling techniques for simulations in lattice gauge theory. 

## Significance and Impact
- Inefficient sampling techniques remains one of the major bottlenecks in the High Energy Physics workflow. Our work offers a significant speedup (≈ x10³) compared to current state-of-the-art methods.

# Research Details
- As simulations approach physical lattice spacing (increasing $\beta$ in **[1]**), conventional methods such as Hamiltonian Monte Carlo (HMC)are known to suffer from _critical slowing down_.
- This causes the computational effort required to generate independent configurations (as measured by $\tau_{\mathrm{int}}$ in **[1]**) to grow exponentially
- Our method generalizes HMC by introducing a series of neural networks which can be trained to generate samples more efficiently, as can be seen in **[1]**.

---
# Old
- As simulations approach physical lattice spacing (increasing β in **[1.]**), conventional techniques suffer from *critical slowing down*.
- This causes the computational effort required to generate independent configurations to grow exponentially (as measured by the integrated auto-correlation time τ in **[1.]**). 
- The ability to efficiently generate independent configurations is currently a major bottleneck for lattice simulations. 
- This work proposes a generalized framework that can be trained to outperform current techniques, as measured by the integrated auto-correlation time of physical quantities.
- By introducing a series of neural networks into the molecular dynamics update of our MCMC integrator, we are able to reduce the sampling cost (compared to existing techniques) by training these networks to encourage efficient exploration of our target distribution.
- The proposed method is able to reduce the computational cost of generating independent configurations by using a trainable kernel to generate proposal configurations.
- Our work demonstrates the usefulness of our approach in 
- Inefficient sampling techniques remain one of the major bottlenecks in the High Energy Physics Workflow.
