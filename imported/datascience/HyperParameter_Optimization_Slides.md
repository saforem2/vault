---
title: "Hyper Parameter Optimization with DeepHyper"
center: true
transition: slide
controls: false
---

# HyperParameter Search

### with [DeepHyper](https://deephyper.readthedocs.io)

[**Prasanna Balaprakash**](https://www.mcs.anl.gov/~/pbalapra/)
<small style="float;text-align:left;">

Computer Scientist
    
Math & Computer Science Division
    
Leadership Computing Facility
    
Argonne National Laboratory
    
</small>
<a href="(https://github.com/deephyper/deephyper"><img src="assets/Pasted%20image%2020220210154802.png" width="200" style="align:right;"></a>

---
# Degrees of Freedom in Neural Networks Design for Scientific Data

![](assets/Pasted%20image%2020220210145254.png)
---
# Degrees of Freedom in Neural Networks Design
![](assets/Pasted%20image%2020220210140515.png)
---

# BiLevel Optimization Problem

$$h_{a}^{\ast}, h_{m}^{\ast} = \mathrm{arg max}_{h_{a}, h_{m} \in H_{a}\times H_{m}} \mathcal{M}^{val}_{w^{\ast}} (h_{a}, h_{m})$$
![](assets/Pasted%20image%2020220210140439.png) 

---

# [DeepHyper](http://deephyper.readthedocs.io) Overview
- Documentation can be found at [deephyper.readthedocs.io](https://deephyper.readthedocs.io)
    
![](assets/Pasted%20image%2020220210162004.png)

---
# Bayesian Optimization

![](assets/Pasted%20image%2020220210161622.png)
---
# [DeepHyper](http://deephyper.readthedocs.io) Overview
![](assets/Pasted%20image%2020220210140822.png)

---
# Configuring Neural Architecture Search
![](assets/Pasted%20image%2020220210193913.png)
---
# DeepHyper NAS-API
![](assets/Pasted%20image%2020220210162802.png)
---
# DeepHyper NAS-API
![](assets/Pasted%20image%2020220210141106.png)
---
# Exploring Search Space
- Regularized ageing evolution to explore the search space of possible architectures
![](assets/Pasted%20image%2020220210163214.png)
---
# Searching for a Surrogate LSTM:
## Sea Surface Temperature Forecasting
![](assets/Pasted%20image%2020220210141204.png)
---
# Scaling
**Single Node, Cluster, Leadership Class**
![](assets/Pasted%20image%2020220210141235.png)
---
# The DeepHyper Project
> "Automated development of machine learning algorithms to support scientific applications"
![](assets/Pasted%20image%2020220210141314.png)
---
# DeepHyper Community
![](assets/Pasted%20image%2020220210141422.png)
---
# References
- P. Balaprakash, M. Salim, T. Uram, V. Vishwanath, S. M. Wild. DeepHyper: Asynchronous hyperparameter search for deep neural networks. In 2018 IEEE 25th international conference on high performance computing (HiPC), 2018.
- P. Balaprakash, R. Egele, M. Salim, S. Wild, V. Vishwanath, F. Xia, T. Brettin, and R. Stevens. Scalable reinforcement-learning-based neural architecture search for cancer deep learning research. In Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis, 2019.
- R. Maulik, R. Egele, B. Lusch, and P. Balaprakash. Recurrent Neural Network Architecture Search for Geophysical Emulation. In SC ’20: IEEE/ACM International Conference on High Performance Computing, Networking, Storage and Analysis, 2020.
- R. Egele, P. Balaprakash, I. Guyon, V. Vishwanath, F. Xia, R. Stevens, Z. Liu.  AgEBO-Tabular: Joint neural architecture and hyperparameter search with autotuned data-parallel training for tabular data. In SC21:  International Conference for High Performance Computing, Networking, Storage and Analysis, (in press), 2021.
- R. Egele, R. Maulik, K. Raghavan, P. Balaprakash, B. Lusch. AutoDEUQ: Automated Deep Ensemble with Uncertainty Quantification, (in review), 2021.
---
# Acknowledgements
![](assets/Pasted%20image%2020220211114101.png)
---

<style> 
:root {
    --r-heading-text-transform: None;
}
</style>