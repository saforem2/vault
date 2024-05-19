Dear Dr. Mike Papka,

I am pleased to nominate Samuel Foreman for the Margaret Butler
Postdoctoral Fellowship. Sam is currently a DOE Office of Science
Graduate Student Research (SCGSR) fellow working at ANL to develop ML
techniques to improve the efficiency of lattice gauge theory
simulations.

Sam is a graduate student in high energy physics with Prof. Yannick
Meurice at U. Iowa. He started working with Yannick’s research group
after his first year in graduate school and has made great progress
within the group. He has taken a classes on field theory, gauge theory
and the standard model, and is currently helping to review the notes of
Yannick’s current class on quantum field theory that will be made into a
book.

In addition to his physics background, he has a very strong background
in computing and has programmed in high-level languages like Python all
the way down to the very low level with Verilog used for FPGAs. This
experience is proving valuable in his current code and algorithm
development tasks, and will be help provide an important foundation as
he develops more HPC skills. This preparation has placed him in an
excellent position to work at ANL and contribute to efforts in exascale
computing and other areas.

He has previously studied the application of ML models to cluster update
methods for the Ising model. He has also using convolutional neural
networks to identify the high and low temperature phases from the
configurations. Applying ML methods to the generation of lattice gauge
theory ensembles is a natural extension of this work, which he is making
great progress on.

Lattice gauge theory relies heavily on having efficient techniques for
sampling the gauge field from the appropriate action. The standard
method, Hybrid Monte Carlo (HMC), exhibits a critical slowing down as
the lattice spacing is decreased approaching the continuum limit.
Finding methods to rectify this problem is a major part of the DOE
Exascale efforts for lattice QCD.

This problem is a major challenge that has been studied for many years.
The complete removal of the critical slowing down may be beyond the
reach of the proposed efforts, but we expect that the techniques and
insight developed here will feed into further efforts to improve
sampling methods.

The initial studies of the improved methods will be done with the Python
code using Tensorflow that he is currently working on. This code has
been tested on Theta, though currently just on a single node. Once the
method has been tested and tuned on lattice sizes that will fit on a
node, we will explore schemes to distribute the model over more nodes.
Initially, we will try simply having independent ML models on each node.
This will allow the Python code to easily scale on Theta. Depending on
the success of this approach we will enhance the model as necessary to
achieve the best balance between the complexity of the model and the
efficiency of the simulations.

Once the model has been tested in parallel, Sam will help port the
method from the Python code into the Quantum Expressions (QEX) ECP
framework being developed at ANL. This code uses the relatively new
programming language Nim (https://nim-lang.org/), which offers very
sophisticated metaprogramming facilities that makes it easy to write
expressive high-level DSLs that can then be transformed at compile-time
into efficient code. It currently runs efficiently on Mira and Theta,
and efforts to use Nim to generate CUDA code and to support Aurora have
also been planned.

The existing HMC code in QEX was developed by Xiao-Yong Jin, and is
flexible enough to easily incorporate the generalized HMC update steps
needed. The main effort will go into developing the ML model and
incorporating it into the code. As an alternative to Tensorflow, we will
evaluate the use of the Nim ML framework Arraymancer
(https://github.com/mratsim/Arraymancer). This has all the basic
components needed for the project and should make integration with QEX
very easy.

ALCF has been developing a program in ML and is continuing to look for
ways to expand the reach of ML into new domains. This collaboration
represents an interesting new area of research that will help strengthen
ALCF’s expertise in this area in addition to providing help to
furthering Sam’s research goals.

Continuing this work at ANL would have a significant impact on Sam’s
career. He already has a strong background in theoretical physics and
computational methods. Spending time working on ECP code at ALCF will
allow him to develop a strong HPC background. Few other institutions
would allow him the opportunities in this area that ALCF can. Sam is a
promising young researcher in computational physics and receiving this
fellowship would allow him to develop his computational skills even
further to become a world class computational scientist. I am looking
forward to having the opportunity to continue to work with him.

Sincerely,
