# Experiment

Convenience wrapper for running experiments.

Instantiates an `ExperimentConfig` (`dataclass obj`) by parsing the contents of the `cfg` (`omegaconf.DictConfig` obj), which is built using [Hydra](https://hydra.cc) from the configurations specified in `l2hmc/conf/config.yaml`.

## BaseExperiment
`BaseExperiment`:
	- **Attributes**:
		- 

`BaseExperiment`
  - **Attributes**:
    - `config`: `ExperimentConfig`
    - trainer: `Trainer`
    - loss_fn: `Callable`
    - dynamics: `Dynamics`
    - optimizer: `Optimizer`
    - lattice: `LatticeU1` | LatticeSU3
    - run: Optional[wandb.run] = None
  - **Methods**:
    - `train(self)`: Train model.
    - `eval(self, job_type: str)`: Evaluate trained model. Job type should be one of `['eval', 'hmc']`
    - 
