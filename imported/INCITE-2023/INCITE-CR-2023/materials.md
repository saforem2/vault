# High-Throughput Calculations of Materials Properties at Finite-Temperature

Author: Chris Wolverton

## Notes
- Previous ALCC (ASCR Leadership Computing Challenge) awards, they've fully calculated the 2nd-order FCs for both elemental materials and experimentally reported binary compounds.

- Project conducted in two steps:
	- First, large scale CSLD calculations on elemental solids and experimentally reported binaries
	- Second, performing supercell calculations on a smaller subset of ternary compounds
- All estimated times are based on the most efficient utilization of resources according to their scaling calculations:
	- 780 Core hours per supercell calculation when using 128 nodes for each sub-job
		- up to 5 supercell calculations for 2nd-order FCs
		- 10 supercell calculations for the 3rd-order FCs
		- 10 supercell calculations for the 4th-order FCs

- Milestone 1: The Elements (3.9M Core Hours)
- Milestone 2: Experimentally-Studied Binaries with Simple Structure (12.5M Core Hours)
- Milestone 3: Stable Binaries (88.9M Core Hours)
- Milestone 4: Experimentally-Studied Ternary ABX_3 Compounds (11.7M Core Hours)

- **Computational Readiness**
	- Calculations can be massively parallelized
	- DFT Calculations in `VASP` are MPI parallelized over bands, k-points and plane-wave coefficients
	- **The high level parallelization in CSLD enables the simultaneous calculation of completely independent super cells, such that a large percentage of the resources on THETA (> 20%) can be used at a time for production runs.**
	- `qmpy` acts as a host to spawn independent `VASP`, `CSLD` `phonopy` and `ShengBTE` calculations.
		- All software used within this project is well tested and can be run in a fully automated workflow
	- Performed extensive tests with the methods used in this project using allocations at CORI (NERSC)
	- **The resulting amount of computational resources required is 117.0 M Core Hours (= 1.83 M THETA node-hours)**.

---

## Question 1
Computational experts conduct reviews to gauge the state of readiness of INCITE submittals to effectively utilize the requested Leadership Computing Facility (LCF) resources.  Reviewers focus on the benchmarking data and other information provided in the proposal to assess the need for leading-class systems, readiness to effectively use INCITE resources, and the reasonableness of the computational campaign the authors defined for the proposed production simulations. 

**Need for and Effective Use of INCITE’s Leadership-class Systems**

State one or more of the following that best exemplifies the proposed computational work.  Is the work:

1. Capability computing (use of 20% or more of the system for production runs: individual simulations or ensembles)
2. Data-analytics, AI application or other nontraditional use models
3. Specific architectural requirements (e.g., large memory, GPU’s, file system)
4. Other

Describe the reason for your selection in your assessment.

Assess the need for LCF resources and how effectively the project team can use the requested systems. For example, could the work be performed elsewhere? How well is the application optimized for the resources requested (in terms of efficiency, scalability, convergence of the solution, throughput, data input/output, workflow tools for ensemble runs, etc.)? The most valuable performance data is that which is most related to the proposed work, and ratings should appropriately reflect this.

_For multiple-resource requests,_ please comment on the merit of allocations on each INCITE resource.

### Response
The work described is capability computing (use >20%) of the system for production runs.

As described in the proposal, the high level parallelization in CSLD enables the simultaneous calculation of completely independent supercells, such that a large percentage of the resources on THETA (> 20%) can be used at a time for production runs.

## Question 2
Assess the computational plan (e.g. system and software requirements, milestones, data management, post processing and analysis), project staffing and technical expertise, and the timeliness of the project to begin computing next year.

**Computational Plan**

1. Is the request for resources clearly explained and the amount of time and storage requirements reasonably estimated and associated with relevant project milestones?
2. Does the Personnel Justification and Management Plan clearly articulate who is responsible for application performance? Is the level of effort sufficient?
3. How much time would it take for the project to begin production runs?

### Response
1. Yes, the request for resources are clearly explained and the amount of time and storage requirements are reasonably estimated and associated with the relevant project milestones.
  > In terms of storage requirement, each compound investigated within this project will require roughly 500 MB of disk space for the output data – a total of about 5 TB. Large files such as wave functions and charge densities are written to disk only temporarily, and will be deleted at the end of each calculation. For long-term storage of the data the relevant output files will be stored in the project archive storage area  
2. While the Personnel Justification and Management Plan doe not explicitly indicate who will be responsible for application _performance_, all members of the team have strong backgrounds in HPC and plan to use well-tested / highly efficient (optimized) libraries for their simulations, and have thoroughly investigated performance using allocations at CORI (NERSC)
3. The proposal indicates that the project should be able to start production runs once approved.
  > All software described above have been developed and well tested individually, such that we could start with the executing of the project as soon as it is approved.


## Question 3
The ratings below summarize the scale on which computational readiness of the submittal is assessed. The appropriateness of LCF resources can be either capability computing, defined as using approximately 20% of the LCF resources available, or specific architectural requirements that only can be met by the INCITE program. To receive an assessment of appropriate for LCF resources, the project must utilize key components of the compute resources (e.g. many-core architecture of the KNL on Theta or GPUs on Summit/Polaris/Frontier/Aurora) or the project must have specific memory needs, data storage requirements, or time to solution expectations, etc. that cannot be obtained elsewhere.

Choose a rating that best describes the project’s readiness for **Theta:**

### Response
**5 -** **Ready**

The project is highly appropriate for the requested resource: the planned work could not be accomplished without INCITE resources; the project codes and workflow are already optimized and demonstrated to operate at scale on the requested resource; a clear plan and justification for the requested resources is provided; and the project is ready to begin efficiently computing immediately.

## Question 4
Based on the milestones, required development, input generation, testing, and reviewer experience, how long do you think before the project will be ready to start production runs?

### Response
Based on the information available in the proposal, I would imagine that the team should be able to start production runs upon approval.

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