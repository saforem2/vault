# L2HMC

**Goal**: Draw independent samples from target distribution specified by

$$p(x) \propto e^{-U_{\beta}(x)}$$

Ultimately, we are interested in evaluating the <span class=”red”>tunneling rate</mark> on the trained model (and comparing against HMC as the baseline).

## Algorithm
1. `input:` $x$ (lattice configuration)
    1. Draw momentum $v\sim\mathcal{N}(0, \mathbb{1})$
2. Generate proposal:   $(x'',v'') = \gets \texttt{TransitionKernel}(\xi)$
    1. $v' = \Gamma^{\pm}\left[x, \partial_{x}U\right]$
    2. Update $x$ in two parts:
        1. $x' = m_{A}\odot x + m_{B}\odot\Lambda^{\pm}\left[x, v'\right]$
        2. $x'' = m_{B}\odot x' + m_{A}\odot \Lambda^{\pm}\left[x', v'\right]$
    3. $v'' = \Gamma^{\pm}\left[x'', \partial_{x}U''\right]$
    
    ---
    
   # Detail 
    1. Update $v$:
    $$v' = v \cdot \exp\left[\varepsilon S_{v}\left(x, \partial_{x}U\right)\right] - \frac{\varepsilon}{2} \bigg[\partial_{x} U\cdot \exp\left[\varepsilon Q_{v}\left(x, \partial_{x}U\right)\right] + T_{v}\left(x, \partial_{x}U\right)\bigg]$$
    2. Update $x$:
        1. Update first half:
        $$ x' = m_{A}\odot x + m_{B}\odot \bigg\{v\cdot S_{x}\left[x_{B}, v'\right] + \varepsilon Q_{x}\left[x_{B}, v'\right]\bigg\}$$
        2. Update second half:
        $$ x'' = m_{B}\odot x' + m_{A}\odot \bigg\{v\cdot S_{x}\left[x'_{A}, v'\right] + \varepsilon Q_{x}\left[x'_{A}, v'\right]\bigg\}$$
    3. Update $v$:
    $$v' = v\cdot \exp\left[{\varepsilon S_{v}(x)}\right] + \varepsilon \left\{\partial_{x}U(x)\cdot\exp\left[\varepsilon Q_{v}(x)\right] + T_{v}(x)\right\}$$
   