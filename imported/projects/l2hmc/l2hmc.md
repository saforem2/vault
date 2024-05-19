---
tags: l2hmc
cssClass:
- img-wide
---
<div align="center">
<img src="https://raw.githubusercontent.com/saforem2/l2hmc-qcd/main/assets/logo.svg" width="33%" />
</div>

### Important

- [ ] Fix / refactor `dynamics.merge_directions` option to use `config.dynamics.nleapfrog` directly
	- [ ] Remove `2 * nleapfrog` from HMC implementation
- [ ] Try simple network and change `Adam` parameters
- [ ] $\beta=5$ on $32\times32$ lattice with very simple network
- [ ] Try and see what happens
    - [ ] Try and speedup training, see if its possible??
- [ ] Try and scale up $\beta$
- [ ] Try simplest network possible 
    - [ ] Try and see what the best training performance is that we can achieve
- [ ] <mark style="background: #FFFF00;color:#1c1c1c;font-weight700;">WRITE TESTS !!</mark> 
- [ ] Implement explicit tests for plaquette in $SU(3)$ model #work #l2hmc
- [ ] Low-rank approximations of dense layers  #work #l2hmc #fthmc #important
- [ ] Gauge + Rotation equivariant architectures #work #l2hmc #fthmc #important
- [ ] Try incorporating $SU(3)$ gauge model in 2 and 4D #work #l2hmc #fthmc #important
- [ ] Explicitly transfer weights between `pytorch` and `tensorflow` implementations #work #l2hmc #important
- [ ]  Finish implementing and testing conv. architecture with `ConvolutionConfig` #l2hmc #work
### Completed
- [x] Look at resetting Adam optimizer each time $\beta$ changes during training #l2hmc #important
- [x] Write methods for performing generic HMC in #l2hmc
- [x] Write logic for distributed training #l2hmc
- [x] Write `AnnealingSchedule` object for handling `beta` during training #l2hmc #work #important
- [x] Specify directory structure using Hydra
- [x] Implement logic for saving / restoring models during training #l2hmc #work
- [x] Implement `AnnealingSchedule` for #l2hmc #work
- [x] Test distributed training with #tensorflow and #pytorch #l2hmc #work
- [x]  Modify #tensorflow `Trainer` object to deal with distributed training horovod #l2hmc #work
- [x] Add logic for saving / restoring #tensorflow model after training #l2hmc
- [x] Add logic for saving / restoring #pytorch model after training #l2hmc
- [x] Test distributed training using #horovod for both #pytorch and #tensorflow implementations of #l2hmc 
- [x] Test distributed training using #DDP and #DeepSpeed for #pytorch using #hydra

# Citations
- 
```bibtex
@inproceedings{Foreman:2021ljl,
    author = "Foreman, Sam and Izubuchi, Taku and Jin, Luchang and Jin, Xiao-Yong and Osborn, James C. and Tomiya, Akio",
    title = "{HMC with Normalizing Flows}",
    booktitle = "{38th International Symposium on Lattice Field Theory}",
    eprint = "2112.01586",
    archivePrefix = "arXiv",
    primaryClass = "cs.LG",
    month = "12",
    year = "2021"
}
@inproceedings{Foreman:2021rhs,
    author = "Foreman, Sam and Jin, Xiao-Yong and Osborn, James C.",
    title = "{LeapfrogLayers: A Trainable Framework for Effective Topological Sampling}",
    booktitle = "{38th International Symposium on Lattice Field Theory}",
    eprint = "2112.01582",
    archivePrefix = "arXiv",
    primaryClass = "hep-lat",
    month = "12",
    year = "2021"
}
@inproceedings{Foreman:2021ixr,
    author = "Foreman, Sam and Jin, Xiao-Yong and Osborn, James C.",
    title = "{Deep Learning Hamiltonian Monte Carlo}",
    booktitle = "{9th International Conference on Learning Representations}",
    eprint = "2105.03418",
    archivePrefix = "arXiv",
    primaryClass = "hep-lat",
    month = "5",
    year = "2021"
}
```


## Papers
- [ ] [Gradient Estimators for Normalizing Flows](https://arxiv.org/pdf/2202.01314.pdf) #papers #lattice #su3 
- [ ] [Semi-Discrete Normalizing Flows through Differentiable Tesselation](https://arxiv.org/pdf/2203.06832.pdf) #papers #su3 #lattice


---

# Analysis of Gradients
Write our loss as 

$$\mathbb{E}_{\mathbf{x}_{T}}\left[\mathcal{L}(\mathbf{x}_{T})\right]$$

where $\mathbf{x}_{T} \in \mathbb{R}^{n}$ is the final sample from a $T$ step HMC chain and $\mathcal{L}$ is a generic loss function.


---
# HMC for $SU(3)$ Lattice Gauge Theory
Introduce conjugate momenta $\pi_{\mu}(x)$ which live in the Lie-algebra of $SU(3)$,
$$
\pi_{\mu}(x) = \sum_{i=1}^{8} \omega^{a}_{\mu}(x) t^{a} 
$$
where $t^a$ are the eight generators of $SU(3)$ and $\omega^{a}_{\mu}(x)$ are eight real numbers for each lattice site.

We assume the generators are normalized as 

$$
\mathrm{tr}\left\{t^{a}t^{b}\right\} = \frac{1}{2}{\delta^{ab}}
$$

We can write the Hamiltonian as 

$$
\mathcal{H}\left[\pi_{\mu}(x), U_{\mu}(x)\right] = \sum_{x,\mu}\frac{1}{2}\omega^{a}_{\mu}(x)\omega^{a}_{\mu}(x) + S[U]
$$
which gives the dynamical system

$$
\frac{d}{d\tau} U_{\mu}(x) = i \pi_{\mu}(x)U_{\mu}(x)
$$

$$
\frac{d}{d\tau} \pi_{\mu}(x) = -\partial^{a}_{x, \mu} S\left[U\right] t^{a}
$$

where $\partial^{a}_{x,\mu}$ is the Lie derivative

$$
\partial^{a}_{x, \mu} S[U] = \frac{d}{ds} S[U^{s, a}]\bigg|_{s=0} \quad \text{where}
$$

$$
U^{s, a}_{\nu}(y) =
\begin{cases}
e^{ist^{a}} U_{\mu}(x),& \nu = \mu, x = y \\
U_{\nu}(y), & \text{else}
\end{cases}
$$

Extending the path integral to include the conjugate momenta 

Our partition function becomes

$$
Z = \int [d\pi] [dU] \exp\left[-\mathcal{H}[\pi,U]\right]
$$

## Matrix Definitions
The generators of $SU(3)$ span the $\mathfrak{s}\mathfrak{u}(3)$ algebra which is the set of **traceless  Hermitian** $3\times 3$ matrices.

The generators are given by $t^{(a)} = \lambda_{a} / 2$ where $\lambda_{a}$ are the Gell-Mann matrices:

$$
\begin{aligned}
&\lambda_{1}=\left(\begin{array}{lll}
0 & 1 & 0 \\
1 & 0 & 0 \\
0 & 0 & 0
\end{array}\right), \quad \lambda_{2}=\left(\begin{array}{ccc}
0 & -i & 0 \\
i & 0 & 0 \\
0 & 0 & 0
\end{array}\right), \quad \lambda_{3}=\left(\begin{array}{ccc}
1 & 0 & 0 \\
0 & -1 & 0 \\
0 & 0 & 0
\end{array}\right)\\
&\lambda_{4}=\left(\begin{array}{lll}
0 & 0 & 1 \\
0 & 0 & 0 \\
1 & 0 & 0
\end{array}\right), \quad \lambda_{5}=\left(\begin{array}{ccc}
0 & 0 & -i \\
0 & 0 & 0 \\
i & 0 & 0
\end{array}\right), \quad \lambda_{6}=\left(\begin{array}{lll}
0 & 0 & 0 \\
0 & 0 & 1 \\
0 & 1 & 0
\end{array}\right) \text {, }\\
&\lambda_{7}=\left(\begin{array}{ccc}
0 & 0 & 0 \\
0 & 0 & -i \\
0 & i & 0
\end{array}\right), \quad \lambda_{\mathrm{s}}=\frac{1}{\sqrt{3}}\left(\begin{array}{ccc}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & -2
\end{array}\right) \text {. }
\end{aligned}
$$

and the gamma matrices $\gamma_{\mu}$ are a set of four matrices which satisfy the anti-commutation relation 

$$
\left\{\gamma_{\mu}, \gamma_{\nu}\right\} = 2 \delta_{\mu\nu}\mathbb{I}
$$

## Characteristic Polynomial
$$
\begin{align}
\mathrm{det}\left[\lambda \mathbb{1} - U\right] &= \mathrm{det}
\begin{bmatrix}
\lambda - U_{11} & -U_{12} & -U_{13} \\
-U_{21} & \lambda - U_{22} & -U_{23} \\
-U_{31} & -U_{32} & \lambda  -U_{33}
\end{bmatrix}\\
&= \lambda^{3} + c_{2}\lambda^{2} + c_{1}\lambda + c_{0}
\end{align}
$$
where 
$$
c_{2} = -(U_{11} + U_{22} + U_{33})
$$
$$
c_{1} = U_{11}U_{22} + U_{22}U_{33} + U_{33}U_{11} - U_{12}U_{21} - U_{23}U_{32} - U_{13}U_{31}
$$
$$
c_{0} = -(U_{12}U_{23}U_{31} + U_{13}U_{21}U_{32} + U_{11}U_{22}U_{33} - U_{12}U_{21}U_{33} - U_{13}U_{31}U_{22} - U_{23}U_{32}U_{11})
$$

We can solve the equation

$$
\lambda^{3} + c_{2}\lambda^{2} + c_{1}\lambda + c_{0} = 0
$$

by first transforming it to a depressed cubic ([Equivariant Manifold Flows](https://arxiv.org/pdf/2107.08596.pdf))

$$
t^{3} + p t + q = 0
$$
where we've made the transformation
$$
\begin{align}
t &= x + \frac{c_{2}}{3} \\
p &= \frac{3c_{1} - c^{2}_{2}}{3} \\
q &= \frac{2c^{3}_{2} - 9 c_{2} c_{1} + 27 c_{0}}{27}
\end{align}
$$

From Cardano's formula we can express the cubic roots of the depressed cubic by

$$
\lambda_{1,2,3}=\sqrt[3]{-\frac{q}{2}+\sqrt{\frac{q^{2}}{4}+\frac{p^{3}}{27}}}+\sqrt[3]{-\frac{q}{2}-\sqrt{\frac{q^{2}}{4}+\frac{p^{3}}{27}}}
$$

where the two cubic roots in the above equation are picked such that they multiply to $-\frac{p}{3}$




---
# [Adversarially Training MCMC with Non-Volume Preserving Flows](https://mdpi-res.com/d_attachment/entropy/entropy-24-00415/article_deploy/entropy-24-00415-v2.pdf)

## Forward direction:
1. Update $v$:
$$v' = v + \frac{\varepsilon}{2} T(x)$$
2. Update $x$:
$$x' = x\odot \exp\left[\varepsilon S(v')\right] + T(v')\odot \exp\left[\varepsilon S(v')\right]$$
3. Update $v$:
$$v'' = v' + \frac{\varepsilon}{2} T(x')$$
- $\log\left|\mathcal{J}\right| = \exp\left[\sum_{i} \varepsilon S(v_{i}) \right]$
## Backward Direction:
1. Update $v$:
$$v' = v'' - \frac{\varepsilon}{2}T(x')$$
2. Update $x$:
$$x' = \left(x - T(v')\odot \exp\left[\varepsilon S(v')\right]\right)\odot\exp\left[-\varepsilon S(v')\right]$$
3. Update v:
$$v = v' - \frac{\varepsilon}{2}T(x)$$

- $\log\left|\mathcal{J}\right| = \exp\left[\sum_{i} -\varepsilon S(v_{i}) \right]$

## Loss function and Training Procedure
- Firstly, we run a gradient-based exploration operator to explore the energy function of the target distribution and get some samples to initialize the buffer.
- In `A-NICE-MC`, HMC is chosen as the exploration operator.
- However, in our scheme, we do not need the exploration operator to sample exactly from the target distribution and only need to explore more regions of the target distribution.
- One of the characteristic properties of high-dimensional spaces is that there is much more volume outside any given neighborhood than inside of it.
- In the $D$-dimensional spaces, the additional computational cost of evaluating a gradient compared with evaluating the function itself will typically be a fixed factor independent of $D$, whereas the $D$-dimensional gradient vector conveys $D$ pieces of information compared with the one piece of information given by the function itself.[^1]
-  Therefore, we 

[^1]: Bishop, C.M. Pattern Recognition and Machine Learning; Springer: New York City, NY, USA, 2006.

---
## $\mathrm{SU}(3)$
# Plaquettes


![[Excalidraw/plaquetteUxy#invert]]

<div align="center">
    
    <img src="../../../Excalidraw/plaquetteUtx.svg">
    
</div>
    
    
![[Excalidraw/plaquetteUtx]]




### Topological Charge $Q$
### Field Theoretic Definition
The topological charge of a gauge field can be defined as the four-dimensional integral of the topological charge density. 
In the continuum, this is given by
$$ Q = \int d^{4}x q(x) $$
where $q(x)$ denotes the topological charge density, defined as 
$$q(x) = \frac{1}{32\pi^{2}}\epsilon_{\mu\nu\rho\sigma}\mathrm{Tr}\left[F_{\mu\nu}F_{\rho\sigma}\right]$$
We can discretize $q(x)$ on the lattice as 
$$Q = a^{4}\sum_{x} q_{L}(x)$$
The simplest lattice discretization of $q_{L}$ is based on the simple plaquette and can be written as 
$$q_{L}^{\mathrm{plaq}} = \frac{1}{32\pi^{2}} \epsilon_{\mu\nu\rho\sigma}\mathrm{Tr}\left(C^{\mathrm{plaq}}_{\mu\nu} C^{\mathrm{plaq}}_{\rho\sigma}\right)$$
with 

![[assets/qplaq.svg|450]]


where the square pictorializes the path ordered product of the links lying along the plaquette sides in the $\mu\nu$-plane


## [[001-Areas/work/datascience/Meetings/l2hmc/meeting notes]]
$$
S_{g}= - \frac{\beta}{3}\left[(1 - 8 \,c_{1} )\sum_{x,\nu<\mu} P_{\mu\nu}(x) + c_{1}\sum_{x, \mu\neq\nu} R_{\mu\nu}(x)\right]
$$

$$
Q = \frac{1}{32\pi^{2}}\sum_{\mathbf{x}, t} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left[\hat{F}_{\mu\nu}(\mathbf{x}, t)\hat{F}_{\rho\lambda}(\mathbf{x}, t)\right]
$$

where $\hat{F}_{\mu\nu}(x; m, n) =$

![[Excalidraw/field-strength.svg|400]]

---
# L2HMC

- [ ]  #l2hmc Denote by $M^{\pm} = \left(\begin{smallmatrix}\Gamma^{\pm} & \cdot \\ \cdot & \Lambda^{\pm}\end{smallmatrix}\right)$, with $\xi = \left(\begin{smallmatrix} v\\ x \end{smallmatrix}\right)$ we have that $$\xi^{\pm} = M^{\pm}\xi \Longrightarrow \xi = M^{\mp}\xi^{\pm}$$
---
# $\mathrm{SU}(N)$
$$U(x, \mu) = \exp\left(i \cdot \frac{1}{2}ga\sum_{\alpha=1}^{N^{2}-1}\tau^{\alpha}\mathbf{A}^{\alpha}(x,\mu)\right)$$

where $\tau^{\alpha}$ ($\alpha= 1$, $\ldots$, $N^{2} - 1$) are the fundamental generators of $SU(N)$, $g$ is the coupling constant, and $a$ is the lattice spacing.

The generators of $SU(N)$ obey 

$$
Tr(\tau^{\alpha}\tau^{\beta}) = \frac{1}{2}\delta^{\alpha\beta}
$$

and 

$$
\left[\tau^{\alpha}, \tau^{\beta}\right] = i f^{\alpha\beta\gamma}\tau^{\gamma}
$$

The following commutation relations then follow

$$
\left[\boldsymbol{E}^{\alpha}, \boldsymbol{U}_{i j}\right]=\frac{1}{2} \sum_{k=1}^{N} \tau_{i k}^{\alpha} \boldsymbol{U}_{k j}
$$

$$
\left[\boldsymbol{E}^{\alpha}, \boldsymbol{U}_{i j}^{\dagger}\right]=-\frac{1}{2} \sum_{k=1}^{N} U_{i k}^{\dagger} \tau_{k j}^{\alpha}
$$

$$
\left[\boldsymbol{E}^{\alpha}, \boldsymbol{E}^{\beta}\right]=i f^{\alpha \beta \gamma} \boldsymbol{E}^{\gamma}
$$

where the indices $i, j$ on $\mathbf{U}_{ij}$ refer to the matrix elements of the $N\times N$ matrix. We denote all quantities which contain the operators $\mathbf{E}^{\alpha}$ or $\mathbf{A}^{\alpha}$ in bold font.
The $\mathrm{SU}(N)$ pure gauge Hamiltonian is written

$$
\begin{aligned}
\boldsymbol{H}=& \frac{g^{2}}{2 a}\left[\sum_{r, \mu} \sum_{\alpha}\left(\boldsymbol{E}^{\alpha}(r, \mu)\right)^{2}\right.\\
&\left.+x \sum_{p \in\{\text { plaquettes }\}}\left(2 N-\left(\boldsymbol{Z}(p)+\boldsymbol{Z}^{\dagger}(p)\right)\right)\right]
\end{aligned}
$$

where 
$$
\boldsymbol{Z}(p)=\operatorname{Tr}\left[\boldsymbol{U}(r, \mu) \boldsymbol{U}(r+\mu, \nu) \boldsymbol{U}^{\dagger}(r+\nu, \mu) \boldsymbol{U}^{\dagger}(r, \nu)\right]
$$

and $x = \frac{2}{g^{4}}$.

==The trace in the $\mathbf{Z}(p))$ operator is taken after matrix multiplication of the four $\mathrm{U}$ matrices.==

The first summation in the Hamiltonian sums over all links in the lattice and the summation involving $\mathbf{Z}(p)$ operator sums over all the plaquettes in the lattice.

---

1.  Update $v$: 
$$
v' = \Gamma^{\pm}[v; \zeta_{v}] = v \odot \exp\left[\frac{\varepsilon_{v}}{2} s_{v}(\zeta_{v})\right] - \frac{\varepsilon_{v}}{2}\left[\partial_{x}S(x)\odot \exp(\varepsilon_{v} q_{v}(\zeta_{v}) +t_{v}(\zeta_{v})\right]
$$

2. Update $x$: 
$$
\begin{align}
x' &= \textcolor{#007DFF}{m_{A}} \odot x + \textcolor{#FF5252}{m_{B}} \odot \Lambda^{\pm}[x; \zeta_{x}] \\
&= \textcolor{#007DFF}{m_{A}} \odot x + \textcolor{#FF5252}{m_{B}} \odot \left\{x \odot \exp(\varepsilon_{x} s_{x}(\zeta_{x}) + \varepsilon_{x}\left[ v’_{k} \odot \exp\left(\varepsilon_{x} q_{x}(\zeta_{x})\right)+t_{x}(\zeta_{x})\right] \right\}
\end{align}
$$

3. Update $x$: 
$$
\begin{align}
x'' &= \textcolor{#FF5252}{m_{B}}  \odot x' + \textcolor{#007DFF}{m_{A}} \odot \Lambda^{\pm}[x'; \zeta_{x'}] \\
&= \textcolor{#FF5252}{m_{B}}  \odot x' + \textcolor{#007DFF}{m_{A}} \odot \left\{x' \odot \exp(\varepsilon_{x} s_{x}(\zeta_{x'}) + \varepsilon_{x}\left[ v’_{k} \odot \exp\left(\varepsilon_{x} q_{x}(\zeta_{x'})\right)+t_{x}(\zeta_{x'})\right] \right\}
\end{align}
$$

4.  Update $v$: 
$$
v'' = \Gamma^{\pm}[v'; \zeta_{v'}] = v' \odot \exp\left[\frac{\varepsilon_{v}}{2} s_{v}(\zeta_{v'})\right] - \frac{\varepsilon_{v}}{2}\left[\partial_{x}S(x)\odot \exp(\varepsilon_{v} q_{v}(\zeta_{v'}) +t_{v}(\zeta_{v'})\right]
$$


Let  $A = \begin{pmatrix}\Gamma^{\pm}[v;\zeta_{v}] & 0 \\ 0 & \Lambda^{\pm}[x; \zeta_{x}] \end{pmatrix}$ and $\vec{z} = \begin{pmatrix} v \\ x \end{pmatrix}$.

---