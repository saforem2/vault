# l2hmc-qcd

```
BaseExperiment(cfg):
  Description
    - Convenience wrapper for running experiments.
      Instantiates an ExperimentConfig (dataclass obj) by parsing
      the contents of the cfg (omegaconf.DictConfig obj), which is 
      built using [Hydra](https://hydra.cc) from the configurations 
      specified in l2hmc/conf/config.yaml
  Attributes
    - self.config: ExperimentConfig
    - self.trainer: Trainer
    - self.loss_fn: Callable
    - self.dynamics: Dynamics
    - self.optimizer: Optimizer
    - self.lattice: LatticeU1 | LatticeSU3
    - self.run: Optional[wandb.run]
  Methods
    - train(self): Train model instantiated from self. HMC.
    - evaluate(self, job_type: str): Evaluate trained model.
```
	
	
# Experiment

Convenience wrapper for running experiments.

Instantiates an `ExperimentConfig` (`dataclass obj`) by parsing the contents of the `cfg` (`omegaconf.DictConfig` obj), which is built using [Hydra](https://hydra.cc) from the configurations specified in `l2hmc/conf/config.yaml`.

- Experiment object needs:
	- 

- `BaseExperiment(cfg: omegaconf.DictConfig)`: 
	- **Attributes**:
		- config: `ExperimentConfig`
		- trainer: `Trainer`
		- loss_fn: `Callable`
		- dynamics: `Dynamics`
		- optimizer: `Optimizer`
		- lattice: `LatticeU1` | LatticeSU3
		- run: `Optional[wandb.run] = None`
	- **Methods**:
		- `train(self)`: Train model.
		- `eval(self, job_type: str)`: 
			- Evaluate trained model. Job type should be one of `['eval', 'hmc']`
		- `build_loss(self) -> Callable`


## Trainer
- `Trainer`:


## Group
- `Group`:
    - methods:
        - `mul(a: Tensor, b: Tensor) -> Tensor`
        - `update_gauge(x: Tensor, p: Tensor) -> Tensor`
        - `adjoint(x: Tensor) -> Tensor`
        - `trace(x: Tensor) -> Tensor`
        - `diff_trace(x: Tensor) -> Tensor`
        - `diff2trace(x: Tensor) -> Tensor`
        - `compat_proj(x: Tensor) -> Tensor`
        - `random(shape: list[int]) -> Tensor`
        - `random_momentum(shape:list[int]) -> Tensor`
        - `kinetic_energy(p: Tensor) -> Tensor:`
    - subclasses:
        - `U1Phase(Group)`
        - `SU3(Group)`
    

## Lattice
- `Lattice`
    - methods:
        - 
    - 

