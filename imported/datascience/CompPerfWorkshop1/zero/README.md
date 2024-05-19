# ZeRO Data Parallelism

Modified from: https://huggingface.co/docs/transformers/parallelism

Consider the simple example of 3 layers, each with 3 weights (`Layer A` has `a0`, `a1`, and `a2`, etc.) as shown below

![[Excalidraw/CPW-Layers.svg|right-wrap]]


For input $\mathbf{x} = (x_{1}, x_{2})^{T}$, the output from each layer is then

$$
\mathbf{y}^{A} = \sigma\left(a_{0} + a_{1} x_{1} + a_{2} x_{2}\right)
$$

$$
\mathbf{y}^{B} = \sigma\left(b_{0} + b_{1} y^{A}_{1} + b_{2} y^{A}_{2}\right)
$$

$$
\mathbf{y}^{C} = \sigma\left(c_{0} + c_{1} y^{B}_{1} + c_{2} y^{B}_{2}\right)
$$


If we have 3 GPUs, the Sharded DDP (Zero-DDP) splits the model across them as

![[Excalidraw/CPW-ZeRO-DataSplit.svg]]



![[Excalidraw/CPW-LayerA-Inputs.svg|500]] 

Our goal is to have all three GPUs compute the **full forward pass** on **their** mini-batch, without having to store the entire model on each GPU.

`GPU:0` has `a0` but needs `a1` from `GPU:1` and `a2` from `GPU:2`, as shown below

$$
\mathbf{y}^{A} = \sigma\left(a_{0} + a_{1} x_{1} + a_{2} x_{2}\right)
$$


Each GPU receives as input a minibatch of data and attempts to compute a forward pass of the model. If we first consider `GPU:0`, in order to compute the output from `Layer A`, it needs:

- `a0`  ✅   on  `GPU:0`
- `a1`  ❌   on  `GPU:1`
- `a2`  ❌   on  `GPU:2`

To compute the output from `LayerA` in the forward pass, we can summarize what each GPU has ✅ vs what it needs ❌ 

| <mark class="red">Layer A</mark> | `GPU:0` | `GPU:1` | `GPU:2` |     |
|:--------------------------------:|:-------:|:-------:|:-------:| --- |
|               `a0`               |   ✅    |   ❌    |   ❌    |     |
|               `a1`               |   ❌    |   ✅    |   ❌    |     |
|               `a2`               |   ❌    |   ❌    |   ✅    |     |

| <mark class="green">Layer B</mark> | `GPU:0` | `GPU:1` |  `GPU:2`    |     |
|:----------------------------------:|:-------:|:-------:|:---:| --- |
|                `b0`                |   ✅    |   ❌    | ❌  |     |
|                `b1`                |   ❌    |   ✅    | ❌  |     |
|                `b2`                |   ❌    |   ❌    | ✅  |     |
|   

| <mark class="blue">Layer C</mark> | `GPU:0`     | `GPU:1` | `GPU:2` |     |
|:---------------------------------:|:---:|:-------:|:-------:| --- |
|               `c0`                | ✅  |   ❌    |   ❌    |     |
|               `c1`                | ❌  |   ✅    |   ❌    |     |
|               `c2`                | ❌  |   ❌    |   ✅    |     |



![[Excalidraw/CPW-LayerA-Sync.svg|500]]


Similarly,   `GPU:1` has `a1` but needs `a0` from `GPU:0` and `a2` from `GPU:2` and   similarly for `GPU:2`.  
$$
\mathbf{y}^{B} = \sigma\left(b_{0} + b_{1} y^{A}_{1} + b_{2} y^{A}_{2}\right)
$$

We can perform all three of these communications in parallel as shown below

![[Excalidraw/CPW-LayerA-Sync.svg|400]]  ![[Excalidraw/CPW-LayerB-Sync.svg|400]]  ![[Excalidraw/CPW-LayerC-Sync.svg|400]]


![[Excalidraw/CWP-ZeRO-DataParallelism.svg]]

Once all 3 GPUs have reconstructed `[a0, a1, a2]`, they can compute the forward pass for Layer A:

$$
\mathbf{y}^{A} = \sigma\left(a_{0} + a_{1} x_{1} + a_{2} x_{2} \right)
$$