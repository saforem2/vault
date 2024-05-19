#### Supplementing Recurrent Neural Network Wave Functions with Symmetry and Annealing to Improve Accuracy
- **Decision**: 2 (Strong Accept)

- **Is the paper appropriate for the workshop?** 
	- Yes, the research clearly demonstrates a successful use case for applying machine learning to a physical problem 
	
-   **Does the paper describe work that is novel and/or interesting?**
	-   Yes, the paper builds on previous research while proposing new techniques that are shown to be beneficial to the problem of interest.
	-   ~~In particular, they show that by incorporating symmetry and introducing an annealing schedule during the optimization they are able to improve upon previous results.~~
	- ~~In this work~~ The authors look at using complex Recurrent neural networks (RNNs) as an ansatz for the wave function the two-dimensional Heisenberg model, building on results from [^fn1].
	- In particular, they look at:
	
		1. Incorporating symmetry into the RNN wave functions, explicitly $U(1)$ symmetry
		2. Implementing an (adiabatic) annealing schedule 
	  
	  and demonstrate that these two techniques allow for better estimates of the ground state energy on the 2D lattices. 
	  
  	- The inclusion of annealing is motivated by previous results and has previously been shown to be effective at overcoming local minima during the variational Monte Carlo (VMC) optimization.
  	- Additionally, the authors show that their method is superior to the density matrix renormalization group (DMRG) approach for lattice volumes larger than $12 \times 12$ and up to $16 \times 16$.
  	- For large system sizes on the triangular lattice, they show that their ansatz outperforms DMRG where frustration is known to make the problem challenging.
	
-   **Does the paper adequately describe what will be presented?**
	- Yes, the paper does a good job of outlining the problem and describing the techniques used.
	
- Minor points:
	-  In the caption of Figure 1:
	
	   > The **red arrows** correspond to the zigzag path ...
	   
  	 seems to be incorrect. I think it should read **green arrows**?
	 
	- On lines 86-87 it is not clear how adding symmetry to the ansatz leaves the number of parameters unchanged

	>  We show that enforcing these symmetries in our ansatz allows to obtain a better 
	>   accuracy without adding more parameters.


[^fn1]:  [https://journals.aps.org/prresearch/pdf/10.1103/PhysRevResearch.2.023358](https://journals.aps.org/prresearch/pdf/10.1103/PhysRevResearch.2.023358) 