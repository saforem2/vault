# Smearing Topology with Reweighted Instantons[^1]


Topological charge in 2D is

$$Q = \frac{1}{2\pi} \int dx^{2} F_{\mu\nu}$$

Introduce $Q = \frac{1}{2}$ configuration with most of charge density $q(x) = f_{\mu\nu} \simeq \pi$ **at one site**.

Such a plaquette has links which "wrap" halfway around the group manifold of $U(1)$ as shown below.

This is accomplished by modifying the gauge action $S = S_{g} + \delta S$

$\delta S = - \sum_{x} \alpha \exp\left[-\frac{\left(\left|F_{\mu\nu}(x)\right| - \pi\right)^{2}}{2\theta_{0}^{2}}\right]\delta_{x, x_{0}}$

where $\alpha$ and $\theta_{0}$ are constant, $x_{0}$ is the site where the plaquette angle is _already_ closest to $\pi$

∂∆S ∂Uµ (x) = 2α[|q(x)| −16π 2 ] exp − [ |q(x)| −16π 2 ] 2 2θ 2 0  × ∂ |q(x)| ∂Uµ     x∈H0


[^1]: Inspired from: [Moving topological charge over the Great Wall in the HMC algorithm - INSPIRE](https://inspirehep.net/literature/880847)