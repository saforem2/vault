- `configs.py`

```python
from hydra.utils import instantiate
from dataclasses import dataclass
from typing import Optional, Any
from hydra.core.config_store import ConfigStore
from omegaconf import DictConfig

# Create type-backed dataclasses for individual components

@dataclass
class Augmentation:
    rotation: Optional[Any] = None
    flip: Optional[bool] = False
    randomcrop: Optional[Any] = None

@dataclass
class DataLoader:
    name: str
    path: os.PathLike

@dataclass
class DataConfig:
    loader: DataLoader
    augmentation: Optional[Augmentation] = None

@dataclass
class ModelConfig:
    loss: str | Callable
    name: Optional[str] = None
    metrics: Optional[list[str] | list | str] = None

DEFAULT_EVALUATOR = {
    'method': 'serial'
}

@dataclass
class SearchConfig:
    name: str = 'CBO'
    evaluator: dict = DEFAULT_EVALUATOR
    max_evals: 20


@dataclass
class AppConfig:
    data: DataConfig
    model: ModelConfig


@dataclass class MainConfig:
	app: AppConfig
	search: SearchConfig

cs = ConfigStore.instance()
cs.store(
	name='main_config',
	node=MainConfig
)

@hydra.main(version_base=None, config_path='./conf', config_name='config')
def main(cfg: DictConfig):
	config = instantiate(cfg)
	type(config.app)     # returns AppConfig
	type(config.search)  # returns SearchConfig


if __name__ == '__main__':
	main()
```

- `conf/config.yaml`:

```yaml
# @package _global_
_target_: configs.MainConfig

defaults:
	- _self_
	- app: default
	- search: default
```


- `conf/app/default.yaml`:

```yaml
_target_: configs.AppConfig

data:
  augmentation:
  - rotation
  - flip
  - randomcrop
  loading:
    name: make_train_and_test_sets
    path: pkg://load_data
model:
  name: resnet
  loss: categorical_crossentropy
  metrics:
  - accuracy
```

- `conf/search/default.yaml`:

```yaml
_target_: configs.SearchConfig
name: CBO
evaluator:
  method: serial
max_evals: 20
```