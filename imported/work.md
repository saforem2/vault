# Work
- [ ] Finish TMS Training courses

## Important
- [ ] Organize material for ATPESC
  - [ ] Sync with Kyle about material

## ATPESC
- [ ] `fas:Github` [python-performance-minicourse/03_mcmc.ipynb](https://github.com/henryiii/python-performance-minicourse/blob/master/03_mcmc.ipynb)
	- [ ] [ISciNumPy.dev - ISciNumPy.dev](https://iscinumpy.gitlab.io/)
	- [ ] [Introduction to the CompClass](https://henryiii.github.io/compclass/IntroToJupyterBook)

## Lattice QCD
### `l2hmc-qcd`
  
## Data Science meeting
- [ ] Mention LCRC project request

## MLPerf-HPC Submissions
- [ ] Work on submissions

## DeepHyper
- [ ] [DeepHyper - Library of Standard ML Pipelines - Google Docs](https://docs.google.com/document/d/1GwiIfCwCtGFdBH0VA1prywDHdSgp9UqyDCfx6vl75x8/edit#heading=h.y0m809kes0g0)
- [ ] `fas:Github` [`deephyper/templates`](https://github.com/deephyper/templates)  #github #deephyper
- [ ] `fas:Github` [hydra_notes](https://gist.github.com/saforem2/b11cbd7297a5e0a105ee37936a604c55) #github #deephyper

## 2023 INCITE Computational Readiness (CR) Review
- **Wednesday, July 20**: ALCF/OLCF CR clarification questions due
- **Friday, July 22**: 2022 INCITE Call for Proposals (closes for renewals)
- Testing implementations and performance of fp64 precision on upcoming hardware
---

# IAIFI Summer Workshop
## Sampling Problem in Lattice QCD (Pure Gauge)

$$
S[U] = \frac{1}{3}\sum \mathrm{Re}\left[\mathrm{Tr}\left[U_{\mu\nu}(x)\right]\right]
$$

$$
p(U) \propto e^{-\beta S[U]}
$$

- Element $\Omega$ of gauge group: choice of $SU(3)$ matrix at each node $x$
$$ U_{\mu}(x) \rightarrow \Omega(x) U_{\mu}(x)\Omega(x+\hat{\mu})^{\dagger}$$