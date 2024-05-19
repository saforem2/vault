# MLMC: Machine Learning Monte Carlo for Lattice Gauge Theory

Sam Foreman, Xiao-Yong Jin, James C. Osborn
Created: <% tp.file.creation_date() %>
Modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>

## Introduction


## Background

Want to calculate observables $\mathcal{O}$:

$$\begin{equation}
\left\langle \mathcal{O}\right\rangle \propto \int \left[\mathcal{D} x\right]\, \mathcal{O}(x)\, p(x)
\end{equation}$$
If these were independent, we could approximate the integral as $\left\langle\mathcal{O}\right\rangle \simeq \frac{1}{N}\sum_{n=1}^{N} \mathcal{O}(x_{n})$ with variance

$$\begin{equation}
\sigma_{\mathcal{O}}^{2} = \frac{1}{N}\,\mathrm{Var}\left[\mathcal{O}(x)\right] \Longrightarrow \sigma_{\mathcal{O}} \propto \frac{1}{\sqrt{N}}.
\end{equation}$$

Instead, nearby configurations are correlated, causing us to incur a factor of $\tau_{\mathrm{int}}^{\mathcal{O}}$ in the variance expression

$$\begin{equation}
\sigma_{\mathcal{O}}^{2} = \frac{\tau_{\mathrm{int}}^{\mathcal{O}}}{N} \mathrm{Var}\left[\mathcal{O}(x)\right]
\end{equation}$$

### Hamiltonian Monte Carlo (HMC)

We can use the Hamiltonian Monte Carlo (HMC) algorithm to help reduce these (auto)correlations. 

Specifically, we want to (sequentially) construct a chain of states:

$$\begin{equation}
x_{0} \rightarrow x_{1} \rightarrow x_{i} \rightarrow \cdots \rightarrow x_{N}
\end{equation}$$

such that, as $N \rightarrow \infty$:

$$\begin{equation}
\left\{x_{i}, x_{i+1}, x_{i+2}, \ldots, x_{N}\right\} \xrightarrow[]{N\rightarrow\infty} p(x)
\end{equation}$$

