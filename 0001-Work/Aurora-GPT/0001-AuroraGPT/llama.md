# llama

- From [`universal-ckp: support llama model` #287](https://github.com/microsoft/Megatron-DeepSpeed/pull/287/files/de2ee279cff5785f7e7bd64ae0c008ccd8b844bf#r1392611020):

    > LLAMA architecture integrated into `gpt_model.py` and I don't think there is `megatron/model/llama_model.py`. 
    > At a high level, LLAMA requires the following "architecture-related" flags:
    >
  
    ```bash
    --no-query-key-layer-scaling
    --use-rotary-position-embeddings
    --untie-embeddings-and-output-weights
    --swiglu
    --normalization rmsnorm
    --disable-bias-linear
    ```
    

