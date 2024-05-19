---
date created: Thursday, September 15th 2022, 7:51:47 am
date modified: Monday, September 19th 2022, 7:10:54 am
---

# SDL Workshop (2022)

- [Configure hyperparameters from the CLI — PyTorch Lightning 1.7.6 documentation](https://pytorch-lightning.readthedocs.io/en/stable/common/hyperparameters.html)


## Discussion w/ Romain
### Hyperparameter Management
- Ideas about new features to advertise ?
- F.A.Q page
- make sure problem is well defined

### DeepHyper
- Optional dependencies
    - Makes package easier to install
    - Separation of responsibilities
- [Evaluator](https://deephyper.readthedocs.io/en/develop/_autosummary/deephyper.evaluator.html

```python
# float for single objective optimization
return 42.0
# str with "F" prefix for failed evaluation
return "F_out_of_memory"
# dict
return {"objective": 42.0}
# dict with additional information
return {"objective": 42.0, "num_epochs_trained": 25, "num_parameters": 420000}
# dict with reserved keywords (when @profile decorator is used)
return {"objective": 42.0, "timestamp_start": ..., "timestamp_end": ...}
# tuple of float for multi-objective optimization (will appear as "objective_0" and "objective_1" in the resulting dataframe)
return 42.0, 0.42 
```