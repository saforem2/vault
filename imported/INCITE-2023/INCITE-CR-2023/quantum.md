# Advanced Computing for Correlated Quantum Matter

PI: Thomas A. Maier

# Question 1: 
**Need for and Effective Use of INCITE’s Leadership-class Systems**

> State one or more of the following that best exemplifies the proposed computational work.  Is the work: 
>  1.  capability computing (use of 20% or more of the system for production runs: individual simulations or ensembles)
>  2.  data-analytics, AI application or other nontraditional use models
>  3.  specific architectural requirements (e.g., large memory, GPU’s, file system)
>  4.  other 
> Describe the reason for your selection in your assessment. 
>  - Assess the need for LCF resources and how effectively the project team can use the requested systems. For example, could the work be performed elsewhere? How well is the application optimized for the resources requested (in terms of efficiency, scalability, convergence of the solution, throughput, data input/output, workflow tools for ensemble runs, etc.)? The most valuable performance data is that which is most related to the proposed work, and ratings should appropriately reflect this.

The proposed computational work is capability computing, with production runs using >= 20% of the system(s).

For the initial year of the project, the project requests an allocation on Summit for which their codes are already optimized and tested.

In addition, their DCA++ implementation has been ported to Frontier using the early-access testbed systems (Crusher and Spock), which have been built and tested and should be able to transition with minimal effort when it becomes available.

For the allocation on Frontier, theyported their DCA++ implementation

In addition, their software implementations have been developed / optimized for leadership class computing facilities and should have no 
and their scientific campaign requires many (O(1000)) independent (embarassingly parallel) simulations for the parameter and frequency scans. 

# Question 2:
>**Computational Plan** 
> 1.  Is the request for resources clearly explained and the amount of time and storage requirements reasonably estimated and associated with relevant project milestones?
> 2.  Does the Personnel Justification and Management Plan clearly articulate who is responsible for application performance? Is the level of effort sufficient?
> 3.  How much time would it take for the project to begin production runs?

1. Yes, the request for resources is clearly explained, with time / storage requirements reasonably estimated and in line with the relevant project milestones.
2. Yes, the Personnel Justification and Management Plan clearly articulates who is responsible for application performance.
	1. Maier (PI) is a distinguished staff in the Computational Chemistry and Nanomaterials Sciences group at ORNL, with a background in HPC. He co-developed the DCA method and is head of the development of its implementation in the DCA++ code.

## Notes
- This project aims to understand and reliably predict the rich phenomenology in correlated quantum materials induced by multiple orbital degrees of freedom, geometric frustration, spin-orbit interactions, and $e$-ph coupling.
- Will study these models using implementations of the DQMC, DCA, and DMRG methods that they have **heavily optimized** for **ORNL's Summit** supercomputer
- The use of **leadership computing** will allow them to go well beyond previous work and use cluster and lattice sizes large enough to provide reliable results.
- Using powerful and efficient numerical algorithms, with optimized implementations making full use of leadership computing, this project will push the limits of correlated quantum materials simulations
- **They have been awarded FIVE (5) INCITE allocations for computing time on ORNL's supercomputers over the past nine years.**
- Their scientific campaign requires many $\mathcal{O}(1000)$ independent (embarassingly parallel) simulations for the parameter and frequency scans and hence exhibits ideal scaling up to $\mathcal{O}(1000)$ nodes with excellent performance on Summit.
- **Frontier Port of DCA++**:
	- They have ported DCA++ to the Frontier architecture using the early-access testbed systems Crusher and Spock.
	- The code builds and all the tests run properly.
	- Therefore expect to be able to transition to Frontier with minimal effort when it becomes available.

## Additional:
- They currently have an implementation of a **novel HMC** method for simulating $e$-ph interactions with nearly ideal linear scaling in complexity with system size and temperature, enabling simulations of systems of upwards of 4000 orbitals, an order of magnitude larger than current state of the art.
	- Code is currently availably as an open-source Julia software package that **does not have GPU support**
	- Plan to port to GPU during first year of project

### Computational Readiness
#### Use of Resources Requested
- For **year 1**, requesting an allocation on **Summit**
	- Their codes are curently optimized
	- During year 1, plan to port their codes to Frontier which will then be used in the following years to enable simulations of larger problem sizes.
		- The estimates given for Frontier will be updated in the renewal
- For the **study of cuprate ladders**, they will carry out DCA++ simulations for a seven-orbital Hubbard model (350 Summit node hours)
- $\mathcal{O}(N_{c}^{3} / T^{3})$ scaling in simulated temperature $T$: A full temperature sweep takes approximately 1000 Summit node hours
- $\mathcal{O}(M^{3})$ scaling in the number of orbitals $M$ -> 1100 (8000) node hours for a single temperature sweep for the single (multi)-orbital ladder models in year 1 and 2, respectively, with 20 units cells each
	- Calculations for 5 different charge densities and two different values of the interaction strength $U$, will then require 10,000 Summit node hours in year 1 and 80,000 Summit-equivalent node-hours in year 2.
	
- Will also carry out complementary calculations of the dynamical spin and charge correlation functions for these models using DMRG
	- Will require 50,000 Summit node hours in year 1 and 125,000 Summit-equivalent node-hours in year 2
- ...

### Computational Approach
- Their team has developed state-of-the-art implementations of the DCA, DQMC, and DMRG algorithms that were developed in-house, and that are optimized for use on leadership class computing facilities
- **DCA++**:
	- The DCA++ code implementing this algorithm is written in C++ with template meta-programming techniques to hide architectural complexities in the QMC implementation. We use MPI for inter-node parallelization, std::threads for the multi-threading on the nodes, and CUDA for the hybrid implementation. For the matrix operations inside the QMC solver we use BLAS, LAPACK, and MAGMA libraries.
	- Pre- and post-processing is handled by python scripts, which generate batch and input files, read the data written by the analysis code, and perform the visualization of the results.
- **DQMC**:
	- The DQMC workflow and I/O requirements are the same as those described for the DCA++ application above, with the exception that files are written in plain text format rather than HDF5.
- **DMRG**:
	- The DMRG++ computer program [84] implements the DMRG algorithm in C++, using both virtual inheritance and C++ templates. A model- and geometry-independent engine provides the core DMRG algorithms; the DMRG++ computer program depends on BLAS, LAPACK, pthreads, hdf5, and uses the MAGMA library for matrix-matrix multiplication on the GPU.
	- Our hdf5 backend performs well on lustre or similar filesystems, and the I/O is a small fraction of total walltime. As was the case on Summit, the walltime on Frontier is expected to be of the order of several hours and DMRG++ has a recovery feature if the run is terminated for excessive walltime use.
	
### Parallel Performance
- **DCA++**:
	- DCA++ — As discussed in the previous section, we have tuned the parallel programming model employed in the DCA++ code to perform well on Summit. Most of the computational kernel is now running on the GPU, and we are using a custom thread pool using C++ std::threads with improved intra-process scheduling and asynchronous CPU-GPU communication in the QMC walker and direct GPU-GPU communication between the walker and accumulator.
	-  the computation of two-particle correlation (i.e., the walker and the accumulator do not share the same function that takes advantage of GPU acceleration and remote direct memory access (RDMA) [139]
- ==Our implementation combines OpenACC directives and batched linear algebra computations using the NVIDIA CUBLAS Library.==
	- We can easily convert from the OpenACC directives to using OpenMP 4.5 with target offload directives once compiler support is sufficiently mature.
	- We plan to replace the CUBLAS batched routines with similar routines in the MAGMA library in preparation of Frontier





---

## Question 1
Computational experts conduct reviews to gauge the state of readiness of INCITE submittals to effectively utilize the requested Leadership Computing Facility (LCF) resources.  Reviewers focus on the benchmarking data and other information provided in the proposal to assess the need for leading-class systems, readiness to effectively use INCITE resources, and the reasonableness of the computational campaign the authors defined for the proposed production simulations. 

**Need for and Effective Use of INCITE’s Leadership-class Systems**

State one or more of the following that best exemplifies the proposed computational work.  Is the work:

1.  capability computing (use of 20% or more of the system for production runs: individual simulations or ensembles)
2.  data-analytics, AI application or other nontraditional use models
3.  specific architectural requirements (e.g., large memory, GPU’s, file system)
4.  other

Describe the reason for your selection in your assessment.

Assess the need for LCF resources and how effectively the project team can use the requested systems. For example, could the work be performed elsewhere? How well is the application optimized for the resources requested (in terms of efficiency, scalability, convergence of the solution, throughput, data input/output, workflow tools for ensemble runs, etc.)? The most valuable performance data is that which is most related to the proposed work, and ratings should appropriately reflect this.

_For multiple-resource requests,_ please comment on the merit of allocations on each INCITE resource.

## Question 2
Assess the computational plan (e.g. system and software requirements, milestones, data management, post processing and analysis), project staffing and technical expertise, and the timeliness of the project to begin computing next year.

**Computational Plan**

1.  Is the request for resources clearly explained and the amount of time and storage requirements reasonably estimated and associated with relevant project milestones?
2.  Does the Personnel Justification and Management Plan clearly articulate who is responsible for application performance? Is the level of effort sufficient?
3.  How much time would it take for the project to begin production runs?

## Question 3
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Theta:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 4
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 5
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Polaris:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 6
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 7
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Summit:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 8
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 9
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Frontier:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 10
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 11
Is the reviewer estimated time to begin production runs (Questions 4, 6, 8, 10) consistent with the project's proposed milestones?
- [ ] Yes
- [ ] No

## Question 12
Is there any development/porting/testing required before starting production runs?
- [ ] Yes
- [ ] No


## Question 13
**Confidential Comments to INCITE Program Management.**

Provide any confidential feedback to the INCITE Program Management that would be helpful in making decisions regarding project allocations. Briefly highlight significant concerns and incorrect node-hour calculations that may justify reductions in the project's duration or allocation.


## Question 14
Is there a significant data analytics, learning, or artificial intelligence component to the project?
- [ ] Yes
- [ ] No

## Question 15
If the answer to the Question 14 above is Yes, please list software the proposal plans to use for these components and indicate whether the team demonstrated running this software on the requested resource(s).

## Question 16
Does the proposal use ensemble runs?
- [ ] Yes
- [ ] No

## Question 17
Does the proposal mention an explicit workflow tool?
- [ ] Yes
- [ ] No

## Question 18
If the answer to the Question 17 above is Yes, please list software the proposal plans to use for these components and indicate whether the team demonstrated running this software on the requested resource(s).

## Question 19
If the proposal plans to use accelerators, are they primarily using:
- [ ] CUDA
- [ ] HIP
- [x] SYCL / DPC++
- [ ] OpenACC
- [ ] OpenMP
- [ ] Kokkos
- [ ] RAJA
- [ ] Other
- [ ] Didn't specify
- [ ] None of the above

## Question 20
Does the team develop the code they are proposing to use?
- [ ] Yes
- [ ] No

# Question 21
Does the expected file system usage exceed 100 TB?


## Question 22
Does the project have any data sharing needs?  Are they explicitly stated as an INCITE requirement?  Existing community practice?  To users outside of LCF?

## Question 1
Computational experts conduct reviews to gauge the state of readiness of INCITE submittals to effectively utilize the requested Leadership Computing Facility (LCF) resources.  Reviewers focus on the benchmarking data and other information provided in the proposal to assess the need for leading-class systems, readiness to effectively use INCITE resources, and the reasonableness of the computational campaign the authors defined for the proposed production simulations. 

**Need for and Effective Use of INCITE’s Leadership-class Systems**

State one or more of the following that best exemplifies the proposed computational work.  Is the work:

1.  capability computing (use of 20% or more of the system for production runs: individual simulations or ensembles)
2.  data-analytics, AI application or other nontraditional use models
3.  specific architectural requirements (e.g., large memory, GPU’s, file system)
4.  other

Describe the reason for your selection in your assessment.

Assess the need for LCF resources and how effectively the project team can use the requested systems. For example, could the work be performed elsewhere? How well is the application optimized for the resources requested (in terms of efficiency, scalability, convergence of the solution, throughput, data input/output, workflow tools for ensemble runs, etc.)? The most valuable performance data is that which is most related to the proposed work, and ratings should appropriately reflect this.

_For multiple-resource requests,_ please comment on the merit of allocations on each INCITE resource.

## Question 2
Assess the computational plan (e.g. system and software requirements, milestones, data management, post processing and analysis), project staffing and technical expertise, and the timeliness of the project to begin computing next year.

**Computational Plan**

1.  Is the request for resources clearly explained and the amount of time and storage requirements reasonably estimated and associated with relevant project milestones?
2.  Does the Personnel Justification and Management Plan clearly articulate who is responsible for application performance? Is the level of effort sufficient?
3.  How much time would it take for the project to begin production runs?

## Question 3
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Theta:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 4
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 5
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Polaris:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 6
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 7
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Summit:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 8
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 9
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Frontier:**

**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

**4 -** **Mostly Ready**

The project is very appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; a very high degree of confidence exists that the project code and workflow can transition to efficient operation at scale on the requested resource; a reasonably clear plan and justification for the requested resources has been provided and the project can be computing efficiently within 1 calendar month.

**3 -** **Approaching Ready**

The project is appropriate for the requested resource: the planned work may not be possible without INCITE resources; the project code has several minor technical issues but can be brought to efficient operation at scale on the requested INCITE resource. The project provides a sufficiently clear plan and justification for the requested resources and can be computing efficiently in less than 3 calendar months using project-provided resources plus normal site user support.

**2 -** **Less Than Ready or Aspects Not Appropriate**

Aspects of the project may not be appropriate for the requested resource: the planned work may not require INCITE resources; the project code has significant technical issues that could negatively impact the ability to effectively use INCITE resources. Minor aspects of the project plan or justification for requested resource may be unclear. The project can only be brought to efficient operation at scale on the requested INCITE resource in no less than 6 calendar months using project resources or project resources plus additional implementation support beyond normal site user support.

**1 -** **Not Ready or Not Appropriate**

The project is not appropriate for the requested resource: INCITE resources are not needed to accomplish the goals; the code cannot run efficiently at scale and there are no plans to scale up; or the project has not provided a clear plan or provided insufficient data to gauge computational readiness.

**Resource Not Requested.**

The project did not request this computing resource.

## Question 10
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

## Question 11
Is the reviewer estimated time to begin production runs (Questions 4, 6, 8, 10) consistent with the project's proposed milestones?
- [ ] Yes
- [ ] No

## Question 12
Is there any development/porting/testing required before starting production runs?
- [ ] Yes
- [ ] No


## Question 13
**Confidential Comments to INCITE Program Management.**

Provide any confidential feedback to the INCITE Program Management that would be helpful in making decisions regarding project allocations. Briefly highlight significant concerns and incorrect node-hour calculations that may justify reductions in the project's duration or allocation.


## Question 14
Is there a significant data analytics, learning, or artificial intelligence component to the project?
- [ ] Yes
- [ ] No

## Question 15
If the answer to the Question 14 above is Yes, please list software the proposal plans to use for these components and indicate whether the team demonstrated running this software on the requested resource(s).

## Question 16
Does the proposal use ensemble runs?
- [ ] Yes
- [ ] No

## Question 17
Does the proposal mention an explicit workflow tool?
- [ ] Yes
- [ ] No

## Question 18
If the answer to the Question 17 above is Yes, please list software the proposal plans to use for these components and indicate whether the team demonstrated running this software on the requested resource(s).

## Question 19
If the proposal plans to use accelerators, are they primarily using:
- [ ] CUDA
- [ ] HIP
- [ ] SYCL / DPC++
- [ ] OpenACC
- [ ] OpenMP
- [ ] Kokkos
- [ ] RAJA
- [ ] Other
- [ ] Didn't specify
- [ ] None of the above

## Question 20
Does the team develop the code they are proposing to use?
- [ ] Yes
- [ ] No

# Question 21
Does the expected file system usage exceed 100 TB?


## Question 22
Does the project have any data sharing needs?  Are they explicitly stated as an INCITE requirement?  Existing community practice?  To users outside of LCF?
