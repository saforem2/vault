---
title: VAE-HMC
date created: Saturday, November 5th 2022, 2:44:04 pm
---
# VAE-HMC

- [vae-hmc](https://web.archive.org/web/20211210014921/https://escholarship.org/content/qt1wg9r75h/qt1wg9r75h_noSplash_d29157bf647afc3178919951aecb6162.pdf?t=q0unn4) [pdf](file:///Users/saforem2/Downloads/vae-hmc.pdf)
- Denote the paramters of interest $q_v$ and its latent representation $q_h$.
- Denote the encoder and decoder as:
  $$
    \begin{align}\varphi &: q_{v} \mapsto q_{h} \\
    \psi &: q_{h} \mapsto q'_{v}
    \end{align}
    $$
  where $q'_{v}$ is a reconstruction of $q_{v}$. If the error of the auto-encoder goes to zero, we have:
  $$\psi = \varphi^{-1}: q_{h} \mapsto q_{v}$$
  - Our algorithm is composed of the following three stages:
	  1. Pre-sample a few samples of $q_{v}$ using standard HMC
	  2. Train an auto-encoder to fit the samples, and obtain the fitted encoder $\varphi$ and decoder $\psi$
	  3. Run an VAE-HMC to propose $q^{\ast}_{v} \gets q_{v}$:
		  1. Find $q_{h} = \varphi(q_{v})$
		  2. Propose $q^{\ast}_{h} \gets q_{h}$ by running HMC in the latent space
		  3. Obtain $q^{\ast}_{v} = \psi(q^{\ast}_{h})$

## HMC in Latent Space

- Let $p_{v} \sim \mathcal{N}(0, \mathbb{1})$ denote the momenta conjugate to $q_{v}$
    - In **physical space**: $(q_{v}, p_{v})$
    - In **latent space**: $(q_{h}, p_{h})$, where the auxiliary variable in latent space, $p_{h}$, is constructed from the same encoder:
    $$p_{h} = \varphi(p_{v})$$
- Denote the **target density** $\pi_{q_{v}}(q_{v})$
- Set potential energy of latent space to be negative log of $\pi_{q_{v}}(q_{v})$:
  $$U_{h}(q_{h}) = U_{v}(\psi(q_{h})) = -\log \pi_{q_{v}}(\psi(q_{h}))$$
- We set the kinetic energy as:
  $$ K_{h}(p_{h}) = K_{v}(\psi(p_{h})) = \psi(p_{h})^{T}M^{-1}\psi(p_{h}) / 2$$
- **Hamiltonian Dynamics in Latent Space**:
  $$\begin{align}
    \dot{q_{hi}} &= \partial_{p_{hi}} K_{h}(p_{h}) \\
    \dot{p_{hi}} &= -\partial_{q_{hi}} U_{h}(q_{h})
    \end{align}
    $$


  > [!bomb]+ Notice!
  > Since we still use the same potential energy function from the original space for our inference, this is **not a reparameterization**.
  >
  > If we use the density function of $q_{h}$ induced by $\varphi(q_{v})$ to be the potential energy, we will need to evaluate the corresponding Jacobian factor at each leapfrog step.
  >
  > As long as detailed balance is satisfied in the original (_physical_) space, the MCMC proposal mechanism will be valid


- The corresponding latent parameters are denoted $(q_{h}, p_{h})$, where the auxiliary variable in the latent space is constructed using the same encoder:
  $$p_{h} = \varphi(p_{v})$$
  where $p_{v}\sim \mathcal{N}(0, \mathbb{1})$.
- Let $\pi_{q_{v}}(q_{v})$ denote the target density. The potential energy of the latent space is then the negative log of this density:
  $$U_{h}(q_{h}) = U_{v}(\psi(q_{h})) = -\log \pi_{q_{v}}(\psi(q_{h}))$$
  > [!danger] Same potential energy!
  > This is _not_ a re-parameterization since we still use the potential energy function from the original space for our inference.


## Detailed Balance with Volume Correction

Partition phase space $(q, p)$ into small regions $A_{k}$ with small volumes $V$


