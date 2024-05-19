# ECP-HI Extension

## Timeline

### Q1 (July → Sep 2022):
- Perform scaling benchmarks and studies of performance as Aurora continues to roll-out
	- Test existing implementations on current Intel hardware
	- Track fp64 performance / potential bugs
- Setup explicit testing + automated gitlab CI to track performance across different hardware
- Continue to investigate hyper-parameter optimizations for 2D U(1) model

### Q2 (Oct → Dec 2022):
- Finish implementation / testing of 4D SU(3) model
	- Test HMC and compare observables against known values
	- Continue testing with simple network architectures
- Continue investigating alternative network architectures / data representations
- Comparison between distributed training libraries?
	- Comparison between `pytorch` and `tensorflow` implementations
	- Test multi-node training performance on Polaris / Intel hardware
	- Performance / tradeoffs / advantages of different frameworks

### Q3 (Jan → Mar 2023):
- Explore hybrid data + model parallel training approaches
- Investigate scaling performance of different frameworks
	- `tensorflow` + `horovod`
	- `pytorch` +
		- `DDP`, `DeepSpeed`, `Horovod`
- Scale up 4D SU(3) model, look at performance metrics on available hardware

### Q4 (Apr → Jun 2023):
- Work on integrating ML frameworks / L2HMC model into lattice QCD code
- Investigate performance on Aurora / final test systems (depending on timing)


### Q5 (July → Sep 2023):
- Investigate performance on Aurora (full system)

# Original Timeline
#### Timeline (July 2022- )

July 2022 -- Sep 2023

##### Q1 (July - Sep 2022):
  - Perform scaling benchmarks and studies of performance as Aurora continues to roll-out
	  - Test existing implementations on current Intel hardware, track fp64 performance / potential bugs
	  - Look at scaling performance on ThetaGPU / Polaris, compare performance with Intel hardware releases
	  - Comparison between `pytorch` and `tensorflow` implementations
		- Performance, tradeoffs / advantages of both frameworks
  - Continue to investigate hyper-parameter optimizations
  - Continue exploring alternative network architectures for 2D U(1) model
    - Faster to iterate on
    - Should give intuition as to what _should_ work for 4D SU(3)
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
- Investigate performance on Aurora ?