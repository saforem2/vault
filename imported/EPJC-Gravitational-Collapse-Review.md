# Sequential Monte Carlo with Cross-Validated Neural Networks for Complexity of Hyperbolic Black Hole Solutions in 4D

I was asked to comment on the neural aspects of the manuscript, so I do not discuss the gravitational collapse aspects.

In this work, the authors develop a new formalism based on Sequential Monte Carlo (SMC) and artificial neural networks (NNs) to model the hyperbolic class of the spherical gravitational self-similar solutions of the Einstein-axion-dilation configuration from type IIB string theory in four dimensions.

This is motivated by the desire to analyze the black hole solutions in diverse dimensions, and has also been related to the holographic description of black hole formation.

Since the hyperbolic equations of motion in four dimensions have multiple solutions (and therefore the collapse functions have overlap domains under these solutions), the authors propose using a sequential Monte Carlo (SMC) approach to derive the posterior distribution of the parameters.

The authors mention that:

> "Due to the highly non linear equations of motion of hyperbolic black holes, various authors used a variety of numerical calculations to simplify the equations of motion and parameters of the theory. Hence, due to this reason the authors must have overlooked the measurement errors that are imposed in exploring the parameters through various numerical methods."

Because of this, they propose a new method that allows them to propagate the measurement errors involved in parameter estimation into their statistical models.

Specifically, they use the $l_{2}$ penalized Leave-One-Out cross-validation to stack the NN-based estimates for critical collapse functions. This approach enables them to assign the optimum weights to NN-based estimates, thereby improving their estimate.

In Section 3 (Statistical Methods), the authors present their sequential Monte Carlo (SMC) approach for recursively estimating the posterior distribution, $\pi(\Omega_{0:t}|\mathbf{y}_{1:t})$.

Assuming that each of the variables' observed trajectories follow a Gaussian distribution, they are able to account for the uncertainty of the observed variables in the differential equations.

To incorporate prior knowledge into their estimate they use a Bayesian framework and treat the unknown parameters of the DE system as random variables. This allows them to find the statistical distribution of the unknown parameters (i.e. the posterior distribution) based on the set of observed data.

Equipped with a mechanism for estimating the posterior, they are able to make statistical inferences about the uncertainty in the estimation procedure and to quantify the characteristics of the DE system. The authors note that their estimate of the posterior distribution confirms the deterministic $\alpha$ and $\beta$ solutions found in the literature for the hyperbolic class in four dimensions.

Using SMC to generate samples from the posterior, they then develop NN estimates for the critical collapse functions corresponding to multiple solutions of the equations of motion.

## Specific Issues

> The posterior distribution does provide all possible solutions in estimating the parameter of the equations of motion[^confusing].

[^confusing]: Lines 33--36. Confusing ??

On Page 9, line 28:

> The SMC estimate recursively the posterior distribution $\pi(\Omega_{0:t}|\mathbf{y}_{1:t})$ as a new state of the sequence becomes available such that one does not require to re-compute the previous states of the trajectory.

I'm a bit confused by the wording here ??

On Page 10:

- Line 30: "differential ~~questions~~" --> "differential equations" ??
- Line 32: "multi-layer ~~perception~~" --> "multi-layer perceptron" ??
- Line 39: "consisting $L$ hidden layers" --> "consisting **of** $L$ hidden layers" ??