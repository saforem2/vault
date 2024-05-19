# L2HMC for 4D SU(3) Gauge Theory

- [ ] Pull material from phys4ml-ICLR draft
- [ ] Send minimal writeup to CSD / SciDAC5 Team


## Introduction

To estimate physical quantities of interest, we are often interested in evaluating integrals of the form

$$
\begin{align}
\left\langle\mathcal{O}\right\rangle &= \frac{1}{\mathcal{Z}} \int \mathcal{D} \left[U \right] \,\mathcal{O}\left(U\right) \,e^{-S[U]} \\
&=  \int \mathcal{D}\left[U\right]\, \mathcal{O}(U)\,\, p(U)
\end{align}
$$
where $(p(U) = e^{-S[U]} / {\mathcal{Z}}$ is the target density, and $S[U]$ is the action of our theory.

This integral can be approximated using Markov Chain  Monte Carlo (MCMC) sampling techniques.

We can measure the performance of our sampler by looking at the integrated autocorrelation time $\tau_{\mathcal{O}}$ of a physical observable $\mathcal{O}$.

In particular, traditional sampling techniques such as Hamiltonian Monte Carlo (HMC) are known to suffer from topological freezing[^1], characterized by $\tau_{\mathcal{Q}}\rightarrow \infty$.

## HMC

In particular, we consider the Hamiltonian Monte Carlo technique, which begins by augmenting the state space with a fictitious momentum variable $P$, normally distributed independently of the gauge links $U$, i.e. $P \sim \pi(P)$, and $p(U, P) = p(U)\cdot \pi(P)$.

Our joint distribution can be written as

$$
p(P, U) = \pi(P)\cdot p(U) \propto e^{-\frac{1}{2}\sum P^{2}} \cdot e^{-S[U]} = e^{-\mathcal{H}(P, U)}
$$

This system obeys Hamilton's equations:

$$
\dot{U} = \frac{\partial\mathcal{H}}{\partial P}, \quad\text{and}\quad \dot{P} = -\frac{\partial\mathcal{H}}{\partial U}
$$
which can be integrated along iso-probability contours of $\mathcal{H} = \text{const.}$

The details of this for the 4D SU(3) model are included in.