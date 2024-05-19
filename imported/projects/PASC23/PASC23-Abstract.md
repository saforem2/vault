# PASC23

## Machine Learning Techniques for Modeling Under-Resolved Phenomena in Massively Parallel Simulations: Algorithms/Frameworks/Applications

**Presenter 10**:
_Gender_: male
_Name_: Dr. Sam Foreman
_Affiliation_: Argonne National Laboratory
_Country of the Primary Affiliation_: United States of America
_Presentation Title_: ML / AI Techniques for Probing Finer Spatial Resolutions in Lattice QCD


> [!seealso] Generative Modeling and Efficient Sampling Techniques for Lattice Gauge Theory (2023-04-21)
> - Prepared for DeepFridays, Spring 2023 Seminar Series @ University of Bologna c/o Andrea Asperti
> >[!summary] Abstract:
> > In this talk we describe how ideas from lattice gauge theory / QCD have contributed to recent advances in generative modeling, and look at some ongoing work in this direction. In particular, we consider the problem of efficiently sampling configurations from probability distributions in high-dimensions, and highlight some of the major challenges. We will look at some of the common problems experienced when scaling models to modern supercomputers with thousands of GPUs, and what's next for large-scale distributed training.



> [!INFO] Generative Modeling and Smarter Sampling for Lattice Gauge Theories
In this work we describe how recent advancements in generative modeling have contributed to simulations in lattice gauge theory, and discuss some ongoing work in this direction.

We are interested in generating independent (lattice) gauge configurations, distributed according to a distribution specified by the action of our theory.

In order to reliably predict values which can be experimentally measured, simulations are carried out at different (increasing) spatial resolutions, allowing an extrapolation to the continuum limit.

In this limit, the cost of generating independent configurations using existing techniques are known to scale exponentially, quickly becoming prohibitively expensive and preventing simulations from probing the (large) energy scales necessary to make new predictions.

In this work we present a new technique that uses a generalized version of the Hamiltonian Monte Carlo algorithm, parameterized by weights in a neural network, that can be trained to make these simulations more efficient, thereby decreasing their overall computational cost.




are known to scale exponentially as we approac

This problem is known to scale exponentially in cost with increasing spatial resolution, quickly becoming prohibitively expensive.

While traditional methods using classical simulations are expected to scale exponentially with increasing spatial resolution, we demonstrate that

We consider the problem of sampling independent (lattice) gauge configurations, the cost of which is known to scale exponentially wi


lattice gauge theory model

We consider the problem of generating indepdent gauge resolution, which is known to scale e



Quantum chromodynamics (QCD)

Quantum field theory is the analytical framework on which the Standard Model of Particle Physics, is built.

The standard model of particle physics is (arguably) one of the most precisely-measured, well-understood theories of modern science.

~~Backed by theoretical arguments from lattice quantumchromodynamics, Th,

In particular, quantum chromodynamics (QCD) is a quantum field theory and is responsible for describing the behavior of subatomic particles of the standard model, and is currently our best model

This theory has been experimentally tested and verified to remarkable accuracy, as evidenced (most recently) by the discovery of the Higgs boson in 2012.


Predictions from quantum field theory have been experimentally tested and verified to remarkable precision at particle accelerators all over the world.

This theory has been experimentally tested and verified to remarkable accuracy over the last 50 years, as evidenced by the discovery of t

, which has been verified to remarkable accuracy

In particular, the theory of quantum chromodynamics which governs the behavior of the quarks and gluons in the nucleus, has

While this has been an incredibly productive effort over the past century, progress has stalled in recent years, due partially to the analytical intractability of quantum

While the standard model has proven


Experiments at the Large Hadron Collider and other particle accelerators around the world have provided an unparalleled verification of the theories' predictions, often to a remarkable precision.


Much of this early success was driven by theoretical arguments from lattice field theory, which have
While initially driven by theoretical arguments from lattice field theory,

Unfortunately, we know that the standard model must be incomplete


One of the major challenges in quantum field theory
Simulations in lattice gauge theory are often limited by the ef
Simulating quantum field theories on a lattice has p
Simulating quantum field theories on

One of the major  in lattice gauge theory
In this work we describe how recent advances in generative modeling have helped to improve the efficiency of Markov Chain Monte Carlo (MCMC) simulations in lattice field theory, and discuss ongoing work in this direction. In particular, we