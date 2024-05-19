> The "lead paragraph" is encapsulated with the LaTeX `quotation`
> environment and is formatted as a single paragraph before the first
> section heading. (The `quotation` environment reverts to its usual
> meaning after the first sectioning command.) Note that numbered
> references are allowed in the lead paragraph. The lead paragraph will
> only be found in an article being prepared for the journal *Chaos*.

# Ideas

- Describe method + argue that we need to incorporate physical symmetries into NNs
    - Translation, rotation invariance
    - Gauge equivariance
    - Physical symmetries encode redundant information about system
        - Don't waste time / compute exploring non-advantageous
            regions of parameter space
        -   simplify representation / description of the system
            -   Less resources for same computational performance
            -   Same performance w/ fewer params, simpler models
        -   Local symmetries are gauge symmetries, and gauge symmetries
            are redundancy in the description of the system
            $$\mathrm{ESS} \propto A(x'|x) \propto \delta^{2} \left[\log\frac{p(x)}{q(x)}\right]\propto \,\text{Volume}$$
        -   Roughly: divide lattice into sublattices, assumed to be
            large enough such that fluctuations in each block are
            independent
            -   then, the variance of $\log\frac{p(x)}{q(x)}$ is
                proportional to the number of blocks,
                $\delta\left\langle \log\frac{p}{q} \right\rangle$
-   Physics problem: Sampling gauge configurations
    -   Many approaches:
        -   L2HMC, FTHMC, NTHMC, Akio / Nobu's work, MIT Groups', etc
    -   Many scales:
        -   Physical:
            -   Lattice volume
            -   Physical theory: $U(1)$, $SU(3)$, etc.
            -   Dimensionality of theory: 2D $U(1)$, 4D $SU(3)$, etc.
            -   Variable representation(s), costs of going back and
                forth
            -   Floating point precision
        -   Computational:
            -   Model size, architecture, training cost
            -   Transfer learning, dimensionality reduction, efficient
                representations
-   Large scale (4D LQCD) expensive $\Longrightarrow$ need efficient
    training methods
    -   Symmetry in models, eliminate redundancy / unnecessary
        information
    -   RG Techniques?
    -   Energy based models
    -   Geometric Deep Learning
    -   Neural ODE

# Introduction

To calculate physical quantities of interest, we are interested in evaluating integrals of the form $$\begin{aligned}
\left\langle\mathcal{O}\right\rangle &= \frac{1}{Z} \int \mathcal{D} \left[U \right] \,\mathcal{O}\left(U\right) \,e^{-S[U]} \\
&=  \int \mathcal{D}\left[U\right]\, \mathcal{O}(U)\,\, \pi(U)
\end{aligned}$$ where $\pi(U) = e^{-S[U]} / {Z}$ is the target density, and $S[U]$ is the action of our theory.

This integral can be approximated using Markov Chain Monte Carlo (MCMC) sampling techniques. We can measure the performance of our sampler by looking at the integrated auto-correlation time $\tau_{\mathcal{O}}$ of a physical observable $\mathcal{O}$.

In particular, traditional sampling techniques such as HMC are known to suffer from topological freezing [@CITE], characterized by $\tau_{Q}\rightarrow \infty$.

# HMC

In particular, we consider the Hamiltonian Monte Carlo technique, which begins by augmenting the state space with a fictitious momentum variable $P$, normally distributed independently of $U$, $P \sim \pi(P)$.
Our joint distribution of the $(P, U)$ system can then be written as
$$p(P, U) = \pi(P)\,\pi(U) \propto e^{-\frac{1}{2}\sum P^{2}} e^{-S[U]} = e^{H(P, U)}.$$

This system obeys Hamilton's equations:

$$\dot{U} = \frac{\partial H}{\partial P}, \quad\text{and}\quad \dot{P} = -\frac{\partial H}{\partial U}$$

which can be integrated along iso-probability contours of
$H = \text{const}$.

The details of this for the 4D SU(3) model are included
in [5.1](#subsec:4DSU3){reference-type="ref" reference="subsec:4DSU3"}.

Finally, we can express the MD update for a single leapfrog step as:

1.  Momentum update:
    $\Gamma: P \rightarrow P' = P - \frac{\varepsilon}{2}\, F[U]$

2.  Gauge link update:
    $\Lambda: U \rightarrow U' = e^{i\varepsilon P'}U$

where $F[U]$ is the force term, as defined in [\[eq:force_term\]](#eq:force_term){reference-type="ref" reference="eq:force_term"}.

We construct a trajectory by successively applying these series of updates, followed by a Metropolis-Hastings accept/reject:
$$A(U'|U) = \min\left\{1, \frac{\pi(P',U')}{\pi(P,U)}\left|\frac{\partial (P', U')}{\partial (P, U)}\right|\right\},$$
and $U^{(i+1)} = U'$ with probability $A(U'|U)$, and $U^{(i+1)} = U^{(i)}$ with probability $1 - A(U'|U)$. For generic HMC, the log determinant factor is equal to unity and can be ignored.

# L2HMC {#sec:l2hmc}


![leapfrog-layer-4D-SU3-vertical.light|300](../../../../../../Excalidraw/leapfrog-layer-4D-SU3-vertical.dark.svg)


![The generalized L2HMC update:
$(P, U) \rightarrow (P'', U'')$](assets/leapfroglayer.pdf){#fig:leapfroglayer
width="40%"}

Augment our existing state space by introducing a direction
$d \sim \mathcal{U}(+, -)$ distributed independently of both $P, U$ as
in [@ForemanDeepLearningHamiltonian2021a].

Then, our joint distribution can be written
$p(P, U, \pm) \propto \pi(P)\, \pi(U) \, \mathcal{U}(+, -)$.

To ensure reversibility and tractability in the determinant of the
Jacobian, we split up the gauge links into two separate updates on
complementary subsets, $U_{A} = m_{A} \odot \, U$, and
$U_{B} = m_{B} \odot \, U$, with $U_{A}\cap U_{B} = \emptyset$.

Again, following the approach in CITE L2HMC, DLHMC, etc., we can write
the generalized leapfrog update as [^1] $$\begin{aligned}
  P' &= \Gamma^{\pm}[P, U] \\
  U' &= m_{A} \odot U + m_{B} \odot \Lambda^{\pm}[P', U] \\
  U'' &= m_{A} \odot U' + m_{A} \odot \Lambda^{\pm}[P', U'] \\
  %U'' &= m_{A} \odot\Lambda^{\pm}[P', U'] + m_{B} \odot U' \\
  P'' &= \Gamma^{\pm}[P', U''].
\end{aligned}$$

## Momentum Update {#subsec:momentum_update}

We consider the forward $d=+$ direction, $\Gamma^{+}$, and note that the
reverse $(d=-)$ direction can be obtained by inverting the $d=+$
expression.

$$\begin{aligned}
  P' &= \Gamma^{+}[P, U] \\
  &= P \odot e^{\frac{\varepsilon}{2}\alpha_{P}}
  - \frac{\varepsilon}{2}\left[F\odot e^{\varepsilon \beta_{P}} + \gamma_{P}\right]
\end{aligned}$$

where $\alpha_{P}, \beta_{P}, \gamma_{P} \in \mathfrak{su}(3)$ are outputs from a neural network

$\varphi_{\theta}: (U, F) \rightarrow (\alpha_{P}, \beta_{P}, \gamma_{P})$,

parameterized by weights $\theta$, as shown in [5.1](#subsec:4DSU3)

By introducing the above modifications, we incur a factor of

$$\log\left|\frac{\partial P'}{\partial P}\right| = \frac{\varepsilon}{2}\sum \alpha_{P}$$

in the Metropolis Hastings accept / reject $A(U'|U)$.

## Link Update {#subsec:link_update}

Again, we consider the forward update, and write 

$$\begin{equation}
  U' = \Lambda^{+}[P, U] = e^{i\varepsilon \tilde{P}} U\end{equation}$$  
where

$\tilde{P} = \left[P\odot e^{\varepsilon \beta_{U}} + \gamma_{U}\right] \in \mathfrak{su}(3)$,

and again $\beta_{U}, \gamma_{U}$ are outputs from a neural network
$$\psi_{\theta}: (P, U) \rightarrow (\beta_{U}, \gamma_{U})$$

## Training {#subsec:training}

We construct a loss function using the expected squared charge
difference
$$\mathcal{L}_{\theta}(U, U') = \mathbb{E}\left[A(U'|U)\,\cdot \delta^{2}_{Q}(U, U')\right],$$
where $\delta^{2}_{Q}(U, U')= |Q' - Q|^{2}$ is the squared topological
charge difference between the initial and proposal configurations.

# Appendix

## 4D $SU(3)$ {#subsec:4DSU3}

For the 4D SU(3) lattice gauge theory, we can write the gauge links
$U_{\mu}(x)$ as

$$\begin{aligned}
U_{\mu}(x) &= \exp\left(i \sum_{k=1}^{8} \omega^{k}_{\mu}(x)\, \lambda^{k}\right) \\
&= \exp\left(i Q\right)
\end{aligned}$$

where $Q \in \mathfrak{su}(3)$, $\omega^{k}_{\mu}(x)$ are real fields,
and $\lambda^{k}$ are the generators of $SU(3)$.

For the pure gauge theory, we use the standard Wilson action

$$\begin{aligned}
S_{G} &= \sum_{\substack{x\ \mu > \nu}} \left\{1 - \frac{1}{3}\mathrm{Re}\,\mathrm{Tr} \left[ U_{\mu}(x) \, U_{\nu}(x+\hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu}) \, U^{\dagger}_{\nu}(x)\right]\right\} \
&= - \frac{\beta}{6} \sum_{x} \sum_{\mu>\nu} \mathrm{Tr}\left[ U_{\mu\nu}(x) + U^{\dagger}_{\mu\nu}(x) \right]
\end{aligned}$$

where
$U_{\mu\nu}(x) = U_{\mu}(x)\, U_{\nu}(x + \hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu})\, U^{\dagger}_{\nu}(x)$.

We can introduce conjugate momenta $P^{k}_{\mu}(x)$ to the real fields
$\omega^{k}_{\mu}(x)$.

Writing the momenta in terms of the generators $\lambda^{k}$,

$$P_{\mu}(x) = \sum_{k=1}^{8} P^{k}_{\mu}(x)\, \lambda^{k},$$

we can write the Hamiltonian as

$$\begin{aligned}
H\left[P, U\right] &= \frac{1}{2}\sum_{\substack{x\in\Lambda \\ \mu, k}}\left[P^{k}_{\mu}(x)\right]^{2} + S\left[U\right] \\
&= \sum \mathrm{Tr}\left[P^{2}\right] + S\left[U\right].
\end{aligned}$$

We can write Hamilton's equations as

$$\frac{d \omega^{k}}{dt} = \frac{\partial H}{\partial P^{k}}\quad\text{and}\quad \frac{d P^{k}}{dt} = \frac{\partial H}{\partial \omega^{k}}.$$

Re-writing the first term,

$$\sum_{k=1}^{8} \frac{d\omega^{k}}{dt} \, \lambda^{k} = \sum_{k=1}^{8} P^{k} \lambda^{k} \Longrightarrow \frac{dQ}{dt} = P$$

and discretizing with step size $\varepsilon$, we get

$$\begin{aligned}
Q(\varepsilon) &= Q(0) + \varepsilon P(0) \Longrightarrow \\
-i \log U(\varepsilon) &= -i \log U(0) + \varepsilon P(0) \Longrightarrow \\
U(\varepsilon) &= e^{i \varepsilon P(0)} U(0).
\end{aligned}$$

And similarly for the second of Hamilton's equations,

$$\frac{dP}{dt} = -\sum_{k=1}^{8} \frac{\partial H}{\partial \omega^{k}} \,\lambda^{k} = -\frac{\partial H}{\partial Q} = - \frac{dS}{dQ}.$$

The discretized form gives

$$\begin{aligned}
P(\varepsilon) &= P(0) - \left.\varepsilon \frac{dS}{dQ}\right|_{t=0} \\
&= P(0) - \varepsilon F[U],
\end{aligned}$$

where $F[U] = dS / dQ$ is the force term.

It can be shown ADD CITATION, that the force term can be written as

$$F = \frac{d S}{dQ} = - \frac{1}{\lambda^{2}} \sum_{k} \lambda^{k} \, \mathrm{Tr}\left[ i \left(UA - A^{\dagger}U^{\dagger}\right) \lambda^{k} \right]$$

where $A$ is the sum over staples

$$\begin{aligned}
A = \sum_{\mu\neq\nu}& U_{\mu}(x +\hat{\mu})\, U^{\dagger}_{\mu}(x + \hat{\nu}) \, U^{\dagger}_{\nu}(x) \\ 
&+ \sum_{\mu\neq\nu} U_{-\nu}(x + \hat{\mu})\, U^{\dagger}_{\mu}(x - \hat{\nu})\, U^{\dagger}_{-\nu}(x).
\end{aligned}$$

Since, $i\left(UA - A^{\dagger}U^{\dagger}\right) \in \mathfrak{su}(3)$,
we can write it in terms of the generators $\lambda^{k}$ as
$$\begin{aligned}
\sum_{k} \lambda^{k} \,\mathrm{Tr}\left[ \lambda^{k} \sum_{j} c_{j}\, \lambda^{j}\right] &= \sum_{k}\sum_{j} c_{j}\, \lambda^{j} \,\mathrm{Tr}\left[ \lambda^{k} \, \lambda^{j}\right] \\
&= \frac{1}{2}\sum_{k}\sum_{j} c_{j}\, t^{k}\, \delta_{jk} \\
&= \frac{1}{2}\sum_{k} c_{k} \, t^{k}
\end{aligned}$$

consequently, we can simplify the force term as

$$\begin{equation}
F = \frac{dS_{G}}{dQ} = - \frac{1}{2g^{2}}\, i \, \left(UA - A^{\dagger}U^{\dagger}\right).\end{equation}$$

Finally, we can express the full HMC updates as:

1.  Momentum update: $\Gamma: P \rightarrow P - \varepsilon\, F[U]$

2.  Gauge link update: $\Lambda: U \rightarrow e^{i\varepsilon P}U$

# Topological Charge {#sec:topQ}

In lattice field theory, the topological charge $Q$ is defined as the 4D
integral over spaacetime of the topological charge density $q$. In the
continuum, $$\begin{aligned}
    Q &= \int d^{4}x q(x), \text{ where } \\
    q(x) &= \frac{1}{32\pi^{2}} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left\{ F_{\mu\nu} F_{\rho\lambda} \right\}
\end{aligned}$$.

On the lattice, we choose a discretization[^2] $q_{L}(x)$ such that
$Q = a^{4} \sum_{x} q_{L}(x)$

The most obvious discretization of $q_{L}$ uses the $1\times1$ plaquette
$P_{\mu\nu}(x)$, and can be written as
$$q^{\mathrm{plaq}}_{L}(x) = \frac{1}{32\pi^{2}} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left\{P_{\mu\nu}(x) P_{\rho\lambda}(x)\right\}$$
this has the advantage of being computationally inexpensive, but leads
to lattice artifacts of order $\mathcal{O}(a^{2})$.

[TODO: Add ]{style="color: #FF5252"}

[^1]: Note: The superscript $\pm$ on $\Gamma$, $\Lambda$ correspond to
    the direction $d = \pm \sim \mathcal{U}(+,-)$

[^2]: We are free to choose a specific discretization as long as it
    gives the right continuum limit