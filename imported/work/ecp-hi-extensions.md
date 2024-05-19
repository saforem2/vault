# ECP-HI Extension

With the proposed extension for the ECP-HI funding, I propose to:
- Continue work on l2hmc-qcd, testing on larger lattice volumes and network architectures on full 4D SU(3) model
- Investigate alternative neural network architectures to improve efficiency and model performance
  - Gauge equivariant convolutions
    - with complex floating point dtypes
  - Transformer architectures
  - Graph neural nets
  - Diffusion models
- Perform scaling benchmarks and studies of system performance as Aurora continues to rollout
  - Perform detailed comparisons between existing Nvidia hardware (Polaris) and Intel (Aurora)
  - Comparison between pytorch and tensorflow implementations, advantages / tradeoffs
- Explore hybrid data + model parallel training approaches
  - Horovod (with tensorflow / pytorch)
  - DeepSpeed integration
  - `torch.DDP` (+ investigate FullyShardedDataParallel ?)
  - `tensorflow.dTensor`
- Opportunity to continue looking at scaling and system performance as Aurora continues to rollout
- Testing implementations and performance of fp64 precision on upcoming hardware

## Timeline
July 2022 -- Sep 2023

### Q1 (July -- Sep 2022):
- Perform scaling benchmarks and studies of performance as Aurora continues to roll-out
	- Test existing implementations on current Intel hardware,
	- Track fp64 performance / potential bugs
- Comparison between `pytorch` and `tensorflow` implementations
- Setup gitlab CI / automated tests across different hardware
- Comparison between distributed training libraries?
	- Compare with multi-node Intel hardware
	- Performance, tradeoffs / advantages of different frameworks
- Continue to investigate hyper-parameter optimizations
- Continue exploring different network architectures for 2D U(1) model

### Q2 (Oct -- Dec 2022):
- Finish implementation / testing of 4D SU(3) model
	- Test HMC and compare observables against known values
	- Continue testing with simple network architectures
- Continue investigating alternative network architectures / data representations
	- Permutation invariant network architectures for eigendecomposition of SU(3) links

### Q3 (Jan -- Mar 2023):
- Explore hybrid data + model parallel training approaches
- Investigate scaling performance of different frameworks
	- `tensorflow`
		- `Horovod`
	- `pytorch`
		- `DDP`
		- `DeepSpeed`
		- `Horovod`
- Scale up 4D SU(3) model, look at performance metrics on available hardware

### Q4 (Apr -- Jun 2023):
- Work on integrating ML frameworks / L2HMC model into lattice QCD code
- Investigate performance on Aurora / final test systems (depending on timing)

### Q5 (July -- Sep 2023):
- Investigate performance on Aurora (full system)



#### Timeline (July 2022- )

July 2022 -- Sep 2023

##### Q1 (July - Sep 2022):
  - Perform scaling benchmarks and studies of performance as Aurora continues to roll-out
	  - Test existing implementations on current Intel hardware, track fp64 performance / potential bugs
	  - Look at scaling performance on ThetaGPU / Polaris, compare performance with Intel hardware releases
	  - Comparison between `pytorch` and `tensorflow` implementations?
	  - Comparison between distributed training libraries?
		  - compare with multi-node intel hardware?
		  -  Performance, tradeoffs / advantages of different frameworks
  - Continue to investigate hyper-parameter optimizations
  - Continue exploring alternative network architectures for 2D U(1) model
    - ~~Faster to iterate on~~
    - ~~Should give intuition as to what _should_ work for 4D SU(3)~~
    - Good hParams for U(1) will guide hyper-parameter initialization for 4D SU(3)

##### Q2 (October - Dec 2022):
- Finish implementation / testing of 4D SU(3) model
	- Test HMC and compare observables against known values
	- Continue testing with simple network architectures
- Continue investigating alternative network architectures
  - Gauge equivariant convolutions
	- with complex floating point dtypes?
  - Transformer architectures, multi-headed (self)-attention
  - Graph Neural Nets
	- Equivariant Message Passing Layers
  - Diffusion models
  - Spectral decomposition
	- permutation invariant net architecture for eigendecomposition

##### Q3 (January - March 2023):
- Explore hybrid data + model parallel training approaches
- Investigate scaling performance of different frameworks
  - `tensorflow`
	- `Horovod`
	- `dTensor`
  - `pytorch`:
	- `DDP`
	  - Zero Redundancy Optimizer (`ZeRO`)
	- `Horovod`
	- `DeepSpeed`
- Scale up 4D SU(3) model, look at performance metrics

##### Q4 (April - June 2023):
- Work on integrating ML frameworks / L2HMC model into Lattice QCD code
- Investigate performance on Aurora / final test systems (depending on timing)

##### Q5 (July - Sep 2023):
- Investigate performance on Aurora (full system)


---

# Scratch
## Project Description
- Opportunity to continue looking at scaling and system performance as Aurora continues to rollout
- Testing fp64 precision
- Investigate hybrid model + data parallel training techniques
- Explore possible integrations with new and existing data services for ML on ALCF systems, with L2HMC serving as an example code
- Continued development / testing of ML methods for Lattice QCD ECP project
    - As frameworks continue to be developed / released it will be beneficial to continue tracking model performance as we approach Aurora
    - Scaling studies / benchmarking
    - Explicit comparisons between `pytorch` and `tensorflow` implementations with specific focus on reproducibility
- Continued development / testing of L2HMC on 4D $SU(3)$ lattice gauge theories
- General development towards incorporating DL libraries / ML methods into existing Lattice QCD code, with focus on compatibility with Aurora + Intel GPU


## Timeline
