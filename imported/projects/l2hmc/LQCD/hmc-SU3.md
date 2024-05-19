---
tags: #lattice #su3 #hmc
---

## Normalizing Flows on Manifolds

- **Manifold Normalizing Flow**:
    - Let $(\mathcal{M}, h)$ be a Riemannian manifold. A normalizing flow on $\mathcal{M}$ is a diffeomorphism $f_{\theta}: \mathcal{M} \rightarrow \mathcal{M}$ (parameterized by $\theta$) that transforms a prior density $\rho$ to model density $\rho_{f_{\theta}}$.
    - The model distribution can be computed via the Riemannian change of variables

    $$\rho_{f_{\theta}}(x) = \rho\left(f^{-1}_{\theta}(x)\right)\left|\det_{h} D_{x} f^{-1}_{\theta}\right|$$

- **Manifold Continuous Normalizing Flow**:
    -  A manifold continuous normalizing flow with base point $z$ is a function $\gamma: [0, \infty) \rightarrow \mathcal{M}$ that satisfies the manifold ODE: 
     $$\frac{d\gamma}{dt} = X(\gamma(t), t), \quad \gamma(0) = z$$ 
     
    - We define $F_{X, T}: \mathcal{M}\rightarrow \mathcal{M}$, $z \mapsto F_{X, T}(z)$ to map any base point $z \in \mathcal{M}$ to the value of the CNF starting at $z$, evaluated at time $T$. This function is the (vector field) flow of $X$

##  Equivariance and Invariance

Let $G$ be an isometry subgroup of $M$. We notate the action of an element $g \in G$ on $\mathcal{M}$ by the map $L_{g}: \mathcal{M} \rightarrow \mathcal{M}$

-  **Equivariant and Invariant Functions**:
    -  We say that a function $f: \mathcal{M} \rightarrow \mathcal{N}$ is equivariant if, for all isometries $g_{x}: \mathcal{M}\rightarrow\mathcal{M}$ and $g_{y}: \mathcal{N} \rightarrow \mathcal{N}$, we have $f \circ g_{x} = g_{y} \circ f$.
    -  We say a function $f: \mathcal{M}\rightarrow\mathcal{N}$ is invariant if $f\circ g_{x} = f$
    
- ** Equivariant Vector Fields**:
    - Let $X : \mathcal{M} \times [0, \infty) \rightarrow T\mathcal{M}$, $X(m, t) \in T_{m}\mathcal{M}$ be a time-dependent vector field on manifold $\mathcal{M}$, with base point $x_{0} \in \mathcal{M}$. $X$ is a $G$-equivariant vector field if $\forall (m, t) \in \mathcal{M}\times [0, \infty)$, $X(L_{g}m, t) = (D_{m} L_{g}) X(m, t)$
    
- **Equivariant Flows**: 
    - A flow $f: \mathcal{M} \rightarrow \mathcal{M}$ is equivariant if it commutes with actions from $G$, i.e. we have $L_{g} \circ f$ = $f \circ L_{g}$

- **Invariance of Density**:
    - A density $\rho$ on a manifold $\mathcal{M}$ is $G$-invariant if, for all $g \in G$ and $x \in \mathcal{M}$, $\rho(L_{g}x) = \rho(x)$, where $L_{g}$ is the action of $g$ on $x$
    
    ## Invariant Densities from Equivariant Flows
    1. **$G$-invariant potential** $\Rightarrow$ **$G$-equivariant vector field**
        - Given a $G$-invariant potential function $\Lambda: \mathcal{M}\rightarrow \mathbb{R}$, the vector field $\nabla \Lambda$ is $G$-equivariant
    2. **$G$-equivariant vector field** $\Rightarrow$ **$G$-equivariant flow**
        - A $G$-equivariant vector field on $\mathcal{M}$ uniquely induces a $G$-equivariant flow
    3. **$G$-equivariant flow** $\Rightarrow$ **$G$-invariant density**
        - A $G$-invariant prior $\rho$ and a $G$-equivariant flow $f$, the flow density $\rho_{f}$ is $G$-invariant
    
    


---

# $SU(3)$ case
The action is given as 

$$S_{G} = \beta \sum_{n}\sum_{\mu>\nu}\left\{1 - \frac{1}{3}\mathrm{Re}\mathrm{Tr}\left[U_{\mu}(n) U_{\nu}(n+\hat{\mu})U_{\mu}^{\dagger}(n+\hat{\nu})U_{\nu}^{\dagger}(n)\right]\right\}$$

The first term gives a constant and can be neglected. Consequently, we adopt the action

$$
\begin{aligned}
S_{G} &=-\frac{\beta}{3} \sum_{n} \sum_{\mu>\nu} \operatorname{Re} \operatorname{Tr}\left[U_{\mu}(n) U_{\nu}(n+\hat{\mu}) U_{\mu}^{\dagger}(n+\hat{\nu}) U_{\nu}^{\dagger}(n)\right] \\
&=-\frac{\beta}{6} \sum_{n} \sum_{\mu>\nu} \operatorname{Tr}\left[U_{\mu \nu}(n)+U_{\mu \nu}^{\dagger}(n)\right]
\end{aligned}
$$

where $U_{\mu\nu}(n) = U_{\mu}(n) U_{\nu}(n+\hat{\mu}) U_{\mu}^{\dagger}(n+\hat{\nu})U_{\mu}^{\dagger}(n)$.

The link variable is represented as $U_{\mu}(n) = \exp\left[i A^{a}_{\mu}(n) t^{a}\right]$.

$t^{a}$ is the $SU(3)$ generator satisfying $\mathrm{Tr}[t^{a}t^{b}] = \delta_{ab}$.


Defining as 

$$
\begin{aligned}
\frac{d U_{\mu}(n)}{d \tau} &=i \dot{A}_{\mu}^{a}(n) t^{a} U_{\mu}(n) \equiv i \pi_{\mu}(n) U_{\mu}(n) \\
\pi_{\mu}(n) &=h_{\mu}^{a}(n) t^{a} \quad\left(h_{\mu}^{a}(n) t^{a} \in \mathrm{R}\right)
\end{aligned}
$$

where $\pi_{\mu}(n)$ is a Hermitian and traceless matrix. Since $\dot{A}^{a}_{\mu}(n) = h^{a}_{\mu}(n)$ is a conjugate field to $A^{a}_{\mu}(n)$. Kinetic part is 

$$
\sum_{n,\mu,a} \frac{1}{2} h^{a}_{\mu}(n) = \frac{1}{2}\sum_{n, \mu}\mathrm{Tr}\left[\pi \pi^{\dagger}\right]
$$

Therefore the Hamiltonian is represented as

$$
\begin{aligned}
H[\pi, U] &=\frac{1}{2} \sum_{n, \mu} \operatorname{Tr}\left[\pi \pi^{\dagger}\right]+S_{G} \\
&=\frac{1}{2} \sum_{n, \mu} \operatorname{Tr}\left[\pi \pi^{\dagger}\right]-\frac{\beta}{6} \sum_{n} \sum_{\mu>\nu} \operatorname{Tr}\left[U_{\mu \nu}(n)+U_{\mu \nu}^{\dagger}(n)\right]
\end{aligned}
$$

We need an equation of motion for $H_{\mu}(n)$.

Taking the time derivative of $H$ above gives

$$\dot{H}=\operatorname{Tr}\left[\sum \dot{\pi} \pi-\sum \frac{\beta}{6}\left(\dot{U}_{\mu \nu}(n)+\dot{U}_{\mu \nu}^{\dagger}(n)\right)\right]$$

and 

$$\begin{aligned}%
\sum_{n, \mu>\nu}\left(\dot{U}_{\mu \nu}(n)+\dot{U}_{\mu \nu}^{\dagger}(n)\right) &=\sum_{n, \mu}\left[\dot{U}_{\mu}(n) V_{\mu}^{\dagger}(n)+V_{\mu}(n) \dot{U}_{\mu}^{\dagger}(n)\right] \\
&=\sum_{n, \mu}\left[i \pi_{\mu}(n) U_{\mu}(n) V_{\mu}^{\dagger}(n)-i V_{\mu}(n) U_{\mu}^{\dagger}(n) \pi_{\mu}(n)\right]%
\end{aligned}$$

giving

$$
\dot{H}_{\mu}(n)=-i \frac{\beta}{6}\left[U_{\mu}(n) V_{\mu}^{\dagger}(n)-\text { h.c. }\right]
$$

for which hermiticity of $H_{\mu}(n)$ is satisfied ✅ (although not guaranteed to be traceless).

Requiring the RHS to be traceless, the d.o.f. on both sides becomes the same, and the equation of motion for $H_{\mu}(n)$ becomes

$$
i \dot{H}_{\mu}(n) = -\frac{\beta}{3}\left[U_{\mu}(n)V^{\dagger}(n)\right]_{\mathrm{AT}}
$$

where the subscript $\mathrm{AT}$ denotes "anti-hermitian and traceless".

For an arbitrary matrix $A$, we have that

$$\left[A\right]_{\mathrm{AT}} = \frac{1}{2}\left(A - A^{\dagger}\right) - \frac{1}{6}\mathrm{Tr}\left(A - A^{\dagger}\right)$$

Since we have obtained the canonical equation of motion for $SU(3)$ gauge fields as 

$$
\begin{align}
\dot{U}_{\mu}(n) &= i H_{\mu}(n)U_{\mu}(n)\\
i \dot{H}_{\mu}(n) &= -\frac{\beta}{3}\left[U_{\mu}(n)V^{\dagger}(n)\right]_{\mathrm{AT}}
\end{align}
$$

we can update the gauge field with the hybrid method. First, as the Langevin step, $h^{a}_{\mu}(n)$ is chosen randomly as a Gaussian ensemble with $\langle h^{2}\rangle =1$.

Then as the MD step, $U$ and $H$ are updated according to the above equation of motion.

Discretizing with a finite time step $\varepsilon$,

$$
\begin{align}
U(\tau) &= \exp\left[i \varepsilon H\left(\tau + \frac{\varepsilon}{2}\right)\right]U(\tau)\\
i H\left(\tau + \frac{3}{2}\varepsilon\right) &= H\left(\tau + \frac{1}{2}\varepsilon\right)- \varepsilon \frac{\beta}{3}\left[U_{\mu}(n)V^{\dagger}(n)\right]_{\mathrm{AT}}
\end{align}
$$

where we've omitted the site and direction indices for simplicity.

For $U$, one needs to approximate the matrix exponential by expanding to some degree. To keep the error in MD evolution $\mathcal{O}(\varepsilon^{2})$, we need an expression at least correct to the order of $\varepsilon^{2}$. If this approximation is not sufficient, the updated $U$ goes out of $SU(3)$ and re-unitarization is necessary.




---

# Notes

# Network Inputs
- For the $U(1)$ case, with $\varphi \in [-\pi, \pi]$

$$
U = e^{i \varphi} = \cos \varphi + i \sin \varphi
$$

we can write the normalized Haar measure as $dU = \tfrac{d\varphi}{2\pi}$


To ensure continuity when updating $U' \gets U$, we represent the inputs to the NNs as

## $SU(3)$
- We want to construct a conjugation invariant potential function $\Lambda : SU(3) \rightarrow \mathbb{R}$. 
    - Matrix conjugation preserves eigenvalues
    - $\Rightarrow$ for $\Lambda: SU(3) \mathbb{R}$ to be invariant to matrix conjugation, it must act on the eigenvalues of $x\in SU(3)$ as a multi-set
    


