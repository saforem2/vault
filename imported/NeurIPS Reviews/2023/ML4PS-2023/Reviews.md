# AI4Science @ NeurIPS'23

## Submission 52

### Seeking Truth and Beauty in Flavor Physics with Machine Learning

> [!quote]+ Overall Evaluation
> This work looks at employing machine learning techniques (with suitably chosen loss functions) to address the perceived deficiencies in the Yukawa sector of the Standard Model.
> 
> They demonstrate that their approach gives rise to models which are consistent with the experimental data and are sufficiently elegant, as measured by a quantitative benchmark. Specifically, they focus on the flavor sector and look at two examples of "beautiful" quark textures under two distinct definitions of "beauty" (uniformity and sparsity, respectively).
> 
> They emphasize that this approach should be interpreted as being part of a larger (general) effort of the automated learning of physical laws by a machine.
> 
> Specifically, they assume that there is an existing mathematical framework that accurately describes the system of interest, and focus exclusively on determining the "best" model parameters without sacrificing correctness.
> 
> Overall, this work proposes an interesting approach that looks at quantifying and improving the "beauty" of physical models. This is done by considering different definitions of beauty (e.g. sparsity and uniformity), and running an optimization procedure to then improve it.

## Submission 167

### Deep Learning with Physics Priors as Generalized Regularizers

> [!quote]+ Overall Evaluation
> This work proposes a method for incorporating approximate models as physics priors in model training. This is done by structuring the priors as generalized regularizers, which is shown to significantly improve testing accuracy. This is particularly useful for situations in which there exists an approximate model of the physical system that we would like to try and incorporate into a machine learning model.
> 
> In particular, they use Vapnik's structural risk minimization (SRM) as the inductive principle to cast the generalized regularization as an optimization problem. By structuring the mechanistic model as a generalized regularizer, they are able to incorporate information from the approximate model into the model training.
> 
> They present experimental results based on their method for three different physical systems (ideal / real pendulum, 1D reaction equation, and a 1D convection example). In all but one case, their analysis suggests that their approach improves test accuracy compared to the baseline model.
> 
> Overall, this is a very interesting approach that attempts to tackle the longstanding problem of incorporating world knowledge into machine learning models. The authors do so by reframing physics priors as generalized regularizers and applying Vapnik's structural risk minimization inductive principle to balance complexity vs. accuracy of the resulting model.
> 
> - Minor issues:
>     - [26]: ~~physics odel~~ --> physics **m**odel
>     - [27]: ~~simplied~~ --> sim**p**lified
>     - [71]: In the case the physics prior is an ODE,
>         - maybe:
            > In the case **where** the physics prior is an ODE 
>             ?

## Submission 155

### Transition Path Sampling with Boltzmann Generator-based MCMC Moves

> [!quote]+ Overall Evaluation
> This work looks at a novel technique for transition path sampling (TPS) between two 3D states of a molecular system (alanine dipeptide). In particular, they propose new paths without requiring molecular simulations by operating in the latent space of a normalizing flow which defines a map between the molecule's Boltzmann distribution and a Gaussian distribution.
> 
> To describe a transition path, they use a sequence of time-equidistant 3D atom configurations between two states (A and B). Traditional approaches typically employ MCMC sampling to iteratively sample a new path given the current one which is then either accepted or rejected according to the Metropolis-Hastings (MH) criteria. Because of this, existing approaches are typically slow to converge and produce correlated paths, requiring significant computational effort and ultimately limiting their usefulness.
> 
> Assuming access to a Boltzmann generator for the molecule of interest (as well as the two states at the ends of the transition), they generate MCMC proposals by moving every frame in a path into their latent space. Each frame then has Gaussian noise added to it such that the overall likelihood can be easily evaluated. The Boltzmann generator is then used to return back to configuration space where the likelihood can be evaluated and either accepted or rejected according to the MH criteria.
> 
> An important property of the proposed approach is that it allows for the evaluation of the energy function, $U(x_{i})$ to be evaluated in parallel. This provides an important advantage over traditional molecular dynamics, where these evaluations must be carried out sequentially. They also go on to describe the challenges associated with this approach, and discuss the difficulty in evaluating likelihood ratios for the proposal paths.
> 
> They propose three different options for the latent space path proposal kernel $q_{Z}(\tilde{z} | z)$: (1.) Gaussian noise, (2.) Gaussian Process (GP) with current path as its mean, and (3.) A GP that is adaptively fit to the history of all sampled transition paths (weakly depending on the current path). Its worth noting that all of these proposals are symmetric and therefore will not contribute to the likelihood ratio in the MH accept / reject.
> 
> Ultimately, they find that due to the low acceptance rate of their MCMC steps, they are only able to produce a low amount of paths or a set of paths with low diversity. They discuss the cost / benefit analysis of their different proposal mechanisms, explaining clearly the limitations of each. Overall, their results suggest that the simplest proposal kernel (Gaussian noise in the latent space) is the best choice out of the three.
> 
> Overall, while lacking strong or decisive results, I still believe this is an interesting approach and worth exploring further. The main challenges associated with sequential MCMC (simulation cost, autocorrelations, inability to efficiently explore multi-modal targets) are pervasive, and the investigation of alternative approaches is a worthwhile endeavor.

# GenBio @ NeurIPS'23

## Submission 47

### Genomic Language Model Predicts Protein Co-Regulation and Function

> [!quote]+ Overall Evaluation
This work looks at training a genomic language model (gLM) on metagenomic scaffolds to learn the latent functional and regulatory relationships between genes.
> 
> Their results suggest that this gLM learns contextualized protein embeddings that capture the genomic context and appears to encode functionally relevant information that is of biologically meaningful. They present evidence of the learned contextualized protein embeddings and attention patterns capturing the biologically relevant information.
> 
> In particular, this work supports an important hypothesis, namely, that the genomic context of proteins can be used to aid function prediction. When comparing to a baseline (bidirectional LSTM model), they report significant improvements in both validation pseudo-accuracy (71.9% vs 28%), and absolute accuracy (59.2% vs. 15%).
> 
> Overall, I think this is an interesting experiment that makes progress towards deciphering the relationship between a gene and its genomic context. This is an important area of research, particularly for understanding the functional behavior of genes.


# ML4PS @ NeurIPS'23
## Submission 150

### JETLOV: Enhancing Jet Tree Tagging through Neural Network Learning of Optimal LundNet Variables

> [!quote]+ Overall Evaluation
> Sam  Foreman has uploaded review for JETLOV: Enhancing Jet Tree Tagging through Neural Network Learning of Optimal LundNet Variables
> 
> -- Review Summary --
> 
> 1. Overall evaluation (based on the strengths and weaknesses of the paper, the soundness of the technical claims, the quality of the presentation, and the overall contribution). 
> This work introduces a new framework, JetLOV, a composite of two models which are first trained separately and then put together for further training on the jet tagging.
> 
> They demonstrate that their approach is able to attain comparable jet tagging performance without relying on the pre-computed LundNet variables.
> 
> Alternatively, they allow they train the first component of their model to learn a new set of variables to feed into the second part (LundNet), which is responsible for the tagging. 
> 
> Their results suggest that their new approach achieves the same performance as LundNet with minor variations.
> 
> Following the performance analysis, they turn to investigate the learned variables and compare against the LundNet variables. Through Canonical Correlation Analysis (CCA), they discovered that there seems to be no significant correlation between the two sets of variables. In particular, while the LundNet variables are physically motivated, their learned variables have no physical interpretation. While this may not be strictly necessary for model performance, it does obscure the models' interpretability. This is represented as a trade off between discovering (possibly) novel insights or hints at new physics, it comes at the cost of model comprehension and understanding.
> 
> Overall, this is an interesting approach that effectively leverages recent ideas from the ML community (pre-training, fine-tuning, mixture of experts). In doing so, they are able to achieve equivalent performance with current approaches while also demonstrating novel behavior in the learned variables.            
> 2. Score
> 7: Accept            
> 3. Reviewer's confidence about the evaluation
> 4: You are confident in your assessment, but not absolutely certain. It is unlikely, but not impossible, that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work.

## Submission 180

### Learned Integration Contour Deformation for Signal-to-Noise Improvement in Monte Carlo Calculations

> [!quote]+ Overall Evaluation
> This work looks at learning a complex contour deformation to improve signal-to-noise ratios in the Monte Carlo integration of path integrals.
> 
> This is done by training a neural network to learn a transformation which minimizes the variance of a particular observable, thereby improving the observed signal to noise ratio.
> 
> They propose a method for performing transfer learning to larger lattice volumes, and show that their method improves signal to noise ratios by orders of magnitude for Wilson loops with large area.
> 
> Overall, this is an interesting idea that seems to work well for the model under consideration (three-dimensional SU(2) lattice gauge theory). 

## Submission 42

### `zephyr`: Stitching Heterogeneous Training Data with Normalizing Flows for Photometric Redshift Inference

> [!quote]+ Overall Evaluation
> Sam  Foreman has uploaded review for Zephyr : Stitching Heterogeneous Training Data with Normalizing Flow for Photometric Redshift Inference
>
> -- Review Summary --
> 
> 1. Overall evaluation (based on the strengths and weaknesses of the paper, the soundness of the technical claims, the quality of the presentation, and the overall contribution). 
> This work looks at incorporating normalizing flows into a mixture density estimation framework for photometric redshift inference.
> 
> The authors do a good job of motivating the scientific need for better density estimation techniques from noisy multi-source training data for precision cosmology.
> 
> They describe the idea behind their approach, and go on to demonstrate its ability to  recover the distribution from noisy data on a toy problem (simple distributions in 2D).
> 
> They demonstrate that their proposed approach achieves a much lower scatter and outlier rate when compared to similar methods (`frankenz`, a Bayesian nearest neighbor method, and `EAzY`, a widely-used template-fitting method), and suggest that this may be due to the improved flexibility and expressive power of the flow based approach.
> 
> They also consider `zephyr`'s interpretability in disentangling contributions from heterogeneous datasets, an important component of quality assessment for cosmology analysis.
> 
> Overall, it is a solid contribution.            
> 2. Score
> 7: Accept            
> 3. Reviewer's confidence about the evaluation
> 3: You are fairly confident in your assessment. It is possible that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work. Math/other details were not carefully checked.
> 

## Submission 150

### Generative Diffusion Models for Lattice Field Theory

> [!quote]+ Overall Evaluation
> Sam  Foreman has uploaded review for Generative Diffusion Models for Lattice Field Theory
> 
> -- Review Summary --
> 
> 1. Overall evaluation (based on the strengths and weaknesses of the paper, the soundness of the technical claims, the quality of the presentation, and the overall contribution). 
> This work looks at the connection between generative diffusion models (DM) and stochastic quantization (SQ).
> 
> They propose using a denoising model to generate field configurations, and consider both a simple toy model (0+0-dimensional field theory) and a real scalar field theory.
> 
> By parameterizing the score function for estimating the drift term of the diffusion model, they are able to generate configurations distributed according to an effective action described by the learned drift term.
> 
> For the 0+0-dimensional model, they show that the effective action serves as a good approximation near ɸ ~ 0 for both the single and double-well cases.
> 
> For the real scalar field theory, they demonstrate that their model reproduces the clustering behavior of the broken phase.
> 
> Overall this is a solid contribution that describes the connection between the denoising process of diffusion models and the Langevin dynamics of the stochastic quantization process.
> 
> It would be nice to have included additional details about the network architecture and training procedure.            
> 2. Score
> 8: Strong accept            
> 3. Reviewer's confidence about the evaluation
> 4: You are confident in your assessment, but not absolutely certain. It is unlikely, but not impossible, that you did not understand some parts of the submission or that you are unfamiliar with some pieces of related work.

## Submission 231

### MCMC to Address Model Misspecification in Deep Learning to Classification of Radio Galaxies

> [!quote]+ Overall Evaluation:
This work looks at the "cold posterior effect (CPE)" that has previously been observed in morphological classification of radio galaxies using variational inference based Bayesian Neural Networks (BNNs), and discusses some of the issues and limitations of current approaches.
They suggest that the CPE arises from using a misspecified parametric family for approximating the posterior. In particular, "using a Gaussian parametric family as a variational approximation to the true posterior distribution is a poor assumption and leads to a misspecified model, which gives rise to the CPE."
The need for better uncertainty quantification of radio galaxy classification models is well going to become increasingly important for the vast amounts of data to be expected from the (upcoming) next-generation radio observatories.
By leveraging the asymptotic convergence of HMC to the true target distribution, they hope to build more accurate Bayesian inference techniques with better uncertainty quantification which is known to be important on downstream scientific tasks.
They emphasize the importance of well-calibrated posterior uncertainties in downstream scientific tasks, and suggest leveraging the asymptotic convergence properties of HMC to improve this.
