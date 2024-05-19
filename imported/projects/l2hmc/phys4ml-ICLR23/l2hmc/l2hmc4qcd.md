# Symmetries & Generative Models: Doing More with Less

## Ideas

- Describe method + argue that we need to incorporate physical symmetries into NNs
    - Translation, rotation invariance
    - Gauge equivariance
    - Physical symmetries encode redundant information about system
        - Don't waste time/ compute exploring non-advantageous regions of parameter space
        - simplify representation / description of the system
            - Less resources for same computational performance
            - Same performance w/ fewer params, simpler models
        - Local symmetries do not exist ; local symmetries are gauge symmetries, and gauge symmetries are redundancy in the description of the system
        $$
        \mathrm{ESS} \propto A(x'|x) \propto \delta^{2} \left[\log\frac{p(x)}{q(x)}\right]\propto \,\text{Volume}
        $$
        - Roughly: divide lattice into sublattices, assumed to be large enough such that fluctuations in each block are independent
            - then, the variance of $\log\frac{p(x)}{q(x)}$ is proportional to the number of blocks, $\delta\left[\log \frac{p}{q} \right]\propto \mathrm{Volume}$

- Physics problem: ==Sampling gauge configurations==
    - Many different approaches:
        - L2HMC
        - FTHMC
        - NTHMC
        - Akio / Nobu's work
        - MIT Groups'
        - etc.
    - Many different scales:
        - Physical:
            - Lattice volume
            - Physical theory ($U(1)$, $SU(3)$, etc.)
            - Dimensionality of theory $(2D $U(1)$, 4D $SU(3)$, etc.)
            - Variable representation(s), costs of going back and forth
            - Floating point precision
        - Computational:
            - Model size
            - Architecture
            - Training cost
            - Transfer learning
            - Dimensionality reduction?
            - Efficient representations

- Large scale (4D LQCD) expensive $\Longrightarrow$ need efficient training methods
    - Symmetry in models, eliminate redundancy / unneccessary information
    - RG Techniques?
    - Energy based models
    - Geometric Deep Learning
    - Neural ODE


## Neural Networks

- NN: Non-linear map $f : X \rightarrow Y$, with $f(X) \subset Y$
    - Equivariant under transformation T if:
    $$ f(Tx) = T' f(x) $$
    for any $x \in X$ and some transformation $T'$ acting on $Y$.
    - If $T' = \mathbb{1}$, then $f$ is _invariant_ under $T$.

- Gauge Transformations: Freedom to make local coordinate transformations across some manifold $\mathcal{M}$
    - Gauge transformations of _fields_ $\iff$ _feature maps_
    - Parallel transport to move kernels across $\mathcal{M}$
    - Gauge equivariant CNN is constructed such that the parallel transport of the kernel across $\mathcal{M}$ is independent of choice of path $P$

## Lattice Gauge Theory

- The degrees of freedom are gauge link variables $U_{x,\mu} \in SU\left(N_{c}\right)$, defined along the edge $x + \hat{\mu}$ of a hyper-cubic lattice $\Lambda$

- Gauge links define parallel transport alone the edges of the lattice, and transform as[^1]
$$
U'_{x,\mu} = \Omega_{x}U_{x,\mu}\Omega^{\dagger}_{x+\hat{\mu}},
$$
under a general gauge transformation $\Omega$.



[^1]: Note taking the hermitian conjugate $U^{\dagger}_{x,\mu} = U_{x+\mu, -\mu}$ amounts to reversing the link $U_{x,\mu}$

## HMC

### SU(3)

We consider the standard Wilson action:

$$
S_{G} = \beta \sum_{n}\sum_{\mu>\nu}\left\{1 - \frac{1}{3}\mathrm{Re}\mathrm{Tr}\left[U_{\mu}(n) U_{\nu}(n+\hat{\mu})U_{\mu}^{\dagger}(n+\hat{\nu})U_{\nu}^{\dagger}(n)\right]\right\}
$$

- Write $U$ in terms of generators of $SU(3)$:
$$
U_{\mu}(x) = \exp\left(i\sum_{k=1}^{8}\omega^{k}_{\mu}(x)\,t^{k}\right) = \exp \left(i Q\right)
$$
where $Q \in \mathfrak{su}(3)$, $\omega^{k}_{\mu}(x)$ are real-valued fields, and $t^{k}$ are the generators of $SU(3)$.

- Introduce momenta $P^{k}_{\mu}(x)$ conjugate to the real fields $\omega^{k}_{\mu}(x)$

$$
P_{\mu}(x) = \sum_{k=1}^{8} P^{k}_{\mu}(x)\, t^{k}
$$
use the fact that 

$$
\frac{1}{2}\sum_{\substack{x\in\Lambda \\ \mu, k}} \left[P^{k}_{\mu}(x)\right]^{2} = \sum_{\substack{x\in \Lambda \\ \mu}} \mathrm{Tr}\left[P^{2}_{\mu}(x)\right]
$$
to express the Hamiltonian

$$
\mathcal{H}\left[P, U\right] = \sum \mathrm{Tr}\left[P^{2}\right] + S\left[U\right].
$$

We can use Hamilton's equations to express the dynamics as

$$
\dot{\omega^{k}} = \frac{\partial\mathcal{H}}{\partial P^{k}} = P^{k} \quad\text{and}\quad \dot{P^{k}} = \frac{\partial \mathcal{H}}{\partial \omega^{k}}
$$

rewriting the first expression

$$
\sum_{k=1}^{8} \dot{\omega^{k}} t^{k} = \sum_{i=1}^{8} P^{i} t^{i} \Longrightarrow \dot{Q} = P
$$
discretizing with step size $\varepsilon$

$$
\begin{align}
Q(\varepsilon) &= Q(0) + \varepsilon P(0) \Longrightarrow \\
-i \log U(\varepsilon) &= -i \log U(0) + \varepsilon P(0) \\
\therefore\quad  U(\varepsilon) &= e^{i\varepsilon P(0)}\,\,U(0).
\end{align}
$$

For the second expression, write as 

$$
\dot{P} = -\sum_{k=1}^{8} \frac{\partial \mathcal{H}}{\partial \omega^{k}} t^{k} = -\frac{\partial\mathcal{H}}{\partial Q} = -\frac{ dS}{dQ}.
$$
again, discretizing with step size $\varepsilon$ gives

$$
P(\varepsilon) = P(0) - \varepsilon \left. \frac{dS}{dQ}\right|_{t=0}
$$
where $\frac{dS}{dQ}$ is the _force term_.

- Need method for evaluating $\tfrac{df}{d\omega^{k}}$ for an arbitrary scalar-valued function $f(U)$. 
    - $U \in SU(3) \Longrightarrow$ this is a directional derivative in the direction of $\omega^{k}$, i.e.
    
$$
\frac{d f(U)}{d\omega^{k}} = \left.\frac{d}{d\omega} f\left(\exp\left[i \sum_{j} \omega^{j} t^{j} + i \omega t^{k}\right]\right)\right|_{\omega=0}
$$
which we parameterize as 

$$
\frac{d f(U)}{d\omega^{k}} = \left.\frac{d f(\gamma(\omega))}{d\omega}\right|_{\omega=0}
$$

### Wilson Gauge Action

$$
\begin{align}
S_{G}\left[U\right] &= \frac{2}{g^{2}} \sum_{x\in\Lambda}\sum_{\mu > \nu} \mathrm{Re}\,\mathrm{Tr}\left[\mathbb{1} - U_{\mu}(x) U_{\nu}(x + \hat{\mu}) U^{\dagger}_{\mu}(x + \hat{\nu}) U^{\dagger}_{\nu}(x)\right] \\
&= \frac{1}{g^{2}} \sum_{x\in\Lambda} \sum_{\mu > \nu} \mathrm{Tr}\left[2\mathbb{1} - U_{\mu}(x) U_{\nu}(x + \hat{\mu}) U^{\dagger}_{\mu}(x + \hat{\nu}) U^{\dagger}_{\nu}(x) - U_{\nu}(x) U_{\mu}(x + \hat{\nu}) U^{\dagger}_{\nu}(x + \hat{\mu}) U^{\dagger}_{\mu}(x)\right] \\
&= \frac{1}{g^{2}} \sum_{x \in \Lambda} \sum_{\nu \neq \mu} \mathrm{Tr}\,\,\left[\mathbb{1} - U_{\mu}(x)\, U_{\nu}(x + \hat{\mu}) \, U^{\dagger}_{\mu}(x + \hat{\nu}) \, U^{\dagger}_{\nu}(x)\right]
\end{align}
$$



## L2HMC

To calculate physical quantities of interest, we are interested in evaluating integrals of the form

$$
\begin{align}
\left\langle\mathcal{O}\right\rangle &= \frac{1}{\mathcal{Z}} \int \mathcal{D} \left[U \right] \,\mathcal{O}\left(U\right) \,e^{-S[U]} \\
&=  \int \mathcal{D}\left[U\right]\, \mathcal{O}(U)\,\, p(U)
\end{align}
$$
where $p(U) = e^{-S[U]} / {\mathcal{Z}}$ is the _target density_, and $S[U]$ is the action of our theory.

This integral can be approximated using Markov Chain Monte Carlo (MCMC) sampling techniques.

In particular, we consider the Hamiltonian Monte Carlo technique, which begins by augmenting the state space with a fictitious momentum variable $P$, normally distributed independently of $U$, $P \sim \pi(P)$.

Our joint distribution of the $(P, U)$ system can then be written as 

$$
p(P, U) = \pi(P)\,p(U) \propto e^{-\frac{1}{2}\sum P^{2}} e^{-S[U]} = e^{-\mathcal{H}(P, U)}.
$$

This system obeys Hamilton's equations:

$$
\dot{U} = \frac{\partial\mathcal{H}}{\partial P}, \quad\text{and}\quad \dot{P} = -\frac{\partial \mathcal{H}}{\partial U}
$$

which can be integrated along iso-probability contours of $\mathcal{H} = \text{const}$.

For the 4D SU(3) lattice gauge theory, we can write the gauge links $U_{\mu}(x)$ as

$$
\begin{align}
U_{\mu}(x) &= \exp\left(i \sum_{k=1}^{8} \omega^{k}_{\mu}(x)\, t^{k}\right) \\
&= \exp\left(i Q\right)
\end{align}
$$
where $Q \in \mathfrak{su}(3)$, $\omega^{k}_{\mu}(x)$ are real fields, and $t^{k}$ are the generators of $SU(3)$.

For the pure gauge theory, we use the standard Wilson action

$$
\begin{align}
S_{G} &= \sum_{x} \sum_{\mu > \nu} \left\{1 - \frac{1}{3}\mathrm{Re}\,\mathrm{Tr} \left[ U_{\mu}(x) \, U_{\nu}(x+\hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu}) \, U^{\dagger}_{\nu}(x)\right]\right\} \\
&= - \frac{\beta}{6} \sum_{x} \sum_{\mu>\nu} \mathrm{Tr}\left[ U_{\mu\nu}(x) + U^{\dagger}_{\mu\nu}(x) \right]
\end{align}
$$

where $U_{\mu\nu}(x) = U_{\mu}(x)\, U_{\nu}(x + \hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu})\, U^{\dagger}_{\nu}(x)$.


We can introduce conjugate momenta $P^{k}_{\mu}(x)$ to the real fields $\omega^{k}_{\mu}(x)$.

Writing the momenta in terms of the generators $t^{k}$,

$$
P_{\mu}(x) = \sum_{k=1}^{8} P^{k}_{\mu}(x)\, t^{k},
$$
we can write the Hamiltonian as

$$
\begin{align}
\mathcal{H}\left[P, U\right] &= \frac{1}{2}\sum_{\substack{x\in\Lambda \\ \mu, k}}\left[P^{k}_{\mu}(x)\right]^{2} + S\left[U\right] \\
&= \sum \mathrm{Tr}\left[P^{2}\right] + S\left[U\right].
\end{align}
$$
We can write Hamilton's equations as

$$
\frac{d \omega^{k}}{dt} = \frac{\partial \mathcal{H}}{\partial P^{k}}\quad\text{and}\quad \frac{d P^{k}}{dt} = \frac{\partial \mathcal{H}}{\partial \omega^{k}}.
$$

Re-writing the first term,

$$
\sum_{k=1}^{8} \frac{d\omega^{k}}{dt} \, t^{k} = \sum_{k=1}^{8} P^{k} t^{k} \Longrightarrow \frac{dQ}{dt} = P
$$
and discretizing with step size $\varepsilon$, we get

$$
\begin{align}
Q(\varepsilon) &= Q(0) + \varepsilon P(0) \Longrightarrow \\
-i \log U(\varepsilon) &= -i \log U(0) + \varepsilon P(0) \Longrightarrow \\
U(\varepsilon) &= e^{i \varepsilon P(0)} U(0).
\end{align}
$$

And similarly for the second of Hamilton's equations,

$$
\frac{dP}{dt} = -\sum_{k=1}^{8} \frac{\partial \mathcal{H}}{\partial \omega^{k}} \,t^{k} = -\frac{\partial \mathcal{H}}{\partial Q} = - \frac{dS}{dQ},
$$

and the discretized form gives

$$
\begin{align}
P(\varepsilon) &= P(0) - \left.\varepsilon \frac{dS}{dQ}\right|_{t=0} \\
&= P(0) - \varepsilon F[U]
\end{align}
$$
where $F[U] = dS / dQ$ is the _force term_.

It can be shown ADD CITATION, that the force term can be written as

$$
F = \frac{d S}{dQ} = - \frac{1}{g^{2}} \sum_{k} t^{k} \, \mathrm{Tr}\left[ i \left(UA - A^{\dagger}U^{\dagger}\right) t^{k} \right]
$$

where $A$ is the sum over _staples_

$$
A = \sum_{\mu\neq\nu} U_{\mu}(x +\hat{\mu})\, U^{\dagger}_{\mu}(x + \hat{\nu}) \, U^{\dagger}_{\nu}(x) + \sum_{\mu\neq\nu} U_{-\nu}(x + \hat{\mu})\, U^{\dagger}_{\mu}(x - \hat{\nu})\, U^{\dagger}_{-\nu}(x).
$$

Now, since $i\left(UA - A^{\dagger}U^{\dagger}\right) \in \mathfrak{su}(3)$ (traceless and Hermitian).

We can write an element of $\mathfrak{su}(3)$ in terms of the generators, giving

$$
\begin{align}
\sum_{k} t^{k} \,\mathrm{Tr}\left[ t^{k} \sum_{j} c_{j}\, t^{j}\right] &= \sum_{k}\sum_{j} c_{j}\, t^{j} \,\mathrm{Tr}\left[ t^{k} \, t^{j}\right] \\
&= \frac{1}{2}\sum_{k}\sum_{j} c_{j}\, t^{k}\, \delta_{jk} \\
&= \frac{1}{2}\sum_{k} c_{k} \, t^{k}
\end{align}
$$

consequently, we can simplify the force term as

$$
F = \frac{dS_{G}}{dQ} = - \frac{1}{2g^{2}}\, i \, \left(UA - A^{\dagger}U^{\dagger}\right).
$$
Finally, we can express the full HMC updates as:

- Momentum Update:
    - $P\gets P - \varepsilon\, F[U]$
- Gauge link update:
    - $U\gets e^{i\varepsilon P}U$


Consider modifying the momentum update as in L2HMC,

$$
P \gets \Lambda^{\pm}(P, U)
$$

$$
P\gets P \odot \exp\left(\frac{\varepsilon}{2} \alpha_{v}\right)
- \frac{\varepsilon}{2}\left[F\odot \exp\left(\varepsilon \beta_{v}\right) + \gamma_{v}\right]
$$

where $\alpha_{v}, \, \beta_{v}, \, \gamma_{v} \in \mathfrak{su}(3)$  are the outputs of a neural network $\Gamma: (U, F) \rightarrow (\alpha_{v}, \beta_{v}, \gamma_{v})$.

![leapfrog-layer-2023-01-16.light | center | 500](leapfrog-layer-2023-01-16.light.svg)

## Appendix

For the 4D SU(3) lattice gauge theory, we can write the gauge links $U_{\mu}(x)$ as

$$
\begin{align}
U_{\mu}(x) &= \exp\left(i \sum_{k=1}^{8} \omega^{k}_{\mu}(x)\, \lambda^{k}\right) \\
&= \exp\left(i Q\right)
\end{align}
$$

where $Q \in \mathfrak{su}(3)$, $\omega^{k}_{\mu}(x)$ are real fields, and $\lambda^{k}$ are the generators of $SU(3)$.

For the pure gauge theory, we use the standard Wilson action

$$
\begin{align}
S_{G} &= \sum_{x} \sum_{\mu > \nu} \left\{1 - \frac{1}{3}\mathrm{Re}\,\mathrm{Tr} \left[ U_{\mu}(x) \, U_{\nu}(x+\hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu}) \, U^{\dagger}_{\nu}(x)\right]\right\} \\
&= - \frac{\beta}{6} \sum_{x} \sum_{\mu>\nu} \mathrm{Tr}\left[ U_{\mu\nu}(x) + U^{\dagger}_{\mu\nu}(x) \right]
\end{align}
$$

where $U_{\mu\nu}(x) = U_{\mu}(x)\, U_{\nu}(x + \hat{\mu}) \, U^{\dagger}_{\mu}(x+\hat{\nu})\, U^{\dagger}_{\nu}(x)$.


We can introduce conjugate momenta $P^{k}_{\mu}(x)$ to the real fields $\omega^{k}_{\mu}(x)$.

Writing the momenta in terms of the generators $\lambda^{k}$,

$$
\begin{equation}
P_{\mu}(x) = \sum_{k=1}^{8} P^{k}_{\mu}(x)\, \lambda^{k},
\end{equation}
$$

we can write the Hamiltonian as

$$
\begin{align}
\mathcal{H}\left[P, U\right] &= \frac{1}{2}\sum_{\substack{x\in\Lambda \\ \mu, k}}\left[P^{k}_{\mu}(x)\right]^{2} + S\left[U\right] \\
&= \sum \mathrm{Tr}\left[P^{2}\right] + S\left[U\right].
\end{align}
$$
We can write Hamilton's equations as

$$
\frac{d \omega^{k}}{dt} = \frac{\partial \mathcal{H}}{\partial P^{k}}\quad\text{and}\quad \frac{d P^{k}}{dt} = \frac{\partial \mathcal{H}}{\partial \omega^{k}}.
$$

Re-writing the first term,

$$
\sum_{k=1}^{8} \frac{d\omega^{k}}{dt} \, \lambda^{k} = \sum_{k=1}^{8} P^{k} \lambda^{k} \Longrightarrow \frac{dQ}{dt} = P
$$

and discretizing with step size $\varepsilon$, we get

$$
\begin{align}
Q(\varepsilon) &= Q(0) + \varepsilon P(0) \Longrightarrow \\
-i \log U(\varepsilon) &= -i \log U(0) + \varepsilon P(0) \Longrightarrow \\
U(\varepsilon) &= e^{i \varepsilon P(0)} U(0).
\end{align}
$$

And similarly for the second of Hamilton's equations,

$$
\frac{dP}{dt} = -\sum_{k=1}^{8} \frac{\partial \mathcal{H}}{\partial \omega^{k}} \,\lambda^{k} = -\frac{\partial \mathcal{H}}{\partial Q} = - \frac{dS}{dQ}.
$$

The discretized form gives

$$
\begin{align}
P(\varepsilon) &= P(0) - \left.\varepsilon \frac{dS}{dQ}\right|_{t=0} \\
&= P(0) - \varepsilon F[U],
\end{align}
$$

where $F[U] = dS / dQ$ is the force term.

It can be shown ADD CITATION, that the force term can be written as

$$
\begin{equation}
F = \frac{d S}{dQ} = - \frac{1}{\lambda^{2}} \sum_{k} \lambda^{k} \, \mathrm{Tr}\left[ i \left(UA - A^{\dagger}U^{\dagger}\right) \lambda^{k} \right]
\end{equation}
$$

where $A$ is the sum over staples

$$
A = \sum_{\mu\neq\nu} U_{\mu}(x +\hat{\mu})\, U^{\dagger}_{\mu}(x + \hat{\nu}) \, U^{\dagger}_{\nu}(x) + \sum_{\mu\neq\nu} U_{-\nu}(x + \hat{\mu})\, U^{\dagger}_{\mu}(x - \hat{\nu})\, U^{\dagger}_{-\nu}(x).
$$

Since, $i\left(UA - A^{\dagger}U^{\dagger}\right) \in \mathfrak{su}(3)$, we can write it in terms of the generators $\lambda^{k}$ as

$$
\begin{align}
\sum_{k} \lambda^{k} \,\mathrm{Tr}\left[ \lambda^{k} \sum_{j} c_{j}\, \lambda^{j}\right] &= \sum_{k}\sum_{j} c_{j}\, \lambda^{j} \,\mathrm{Tr}\left[ \lambda^{k} \, \lambda^{j}\right] \\
&= \frac{1}{2}\sum_{k}\sum_{j} c_{j}\, t^{k}\, \delta_{jk} \\
&= \frac{1}{2}\sum_{k} c_{k} \, t^{k}
\end{align}
$$

consequently, we can simplify the force term as

$$
F = \frac{dS_{G}}{dQ} = - \frac{1}{2g^{2}}\, i \, \left(UA - A^{\dagger}U^{\dagger}\right).
$$

Finally, we can express the full HMC updates as:

1. Momentum update: $\Gamma: P \rightarrow P - \varepsilon\, F[U]$
2.  Gauge link update: $\Lambda: U \rightarrow e^{i\varepsilon P}U$


\section{Topological Charge}%
\label{sec:topQ}

In lattice field theory, the topological charge $Q$ is defined as the 4D integral over spaacetime of the topological charge density $q$.

In the continuum,

$$
\begin{align}
    Q &= \int d^{4}x q(x), \text{ where } \\
    q(x) &= \frac{1}{32\pi^{2}} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left\{ F_{\mu\nu} F_{\rho\lambda} \right\}
\end{align}.
$$

On the lattice, we choose a discretization\footnote{We are free to choose a specific discretization as long as it gives the right continuum limit} $q_{L}(x)$ such that $Q = a^{4} \sum_{x} q_{L}(x)$

The most obvious discretization of $q_{L}$ uses the $1\times1$ plaquette $P_{\mu\nu}(x)$, and can be written as

$$
\begin{equation}
    q^{\mathrm{plaq}}_{L}(x) = \frac{1}{32\pi^{2}} \epsilon_{\mu\nu\rho\lambda} \mathrm{Tr}\left\{P_{\mu\nu}(x) P_{\rho\lambda}(x)\right\}
\end{equation}
$$
this has the advantage of being computationally inexpensive, but leads to lattice artifacts of order $\mathcal{O}(a^{2})$.

**Add symmetrized clover-leaf defn**