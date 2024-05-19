---
date created: Monday, September 19th 2022, 8:54:56 am
date modified: Monday, September 19th 2022, 4:48:13 pm
---
# INCITE-2023

- Panel deliverables due by the end of the day
- before departing please give panel notes to observer
- Please destroy any hardcopy materials
- Please take the survey
- Proposals, reviews, and discussions associated with the review process should be treated as confidential

## Quantum Panel
### Proton Spin in Exascale Era: Probing Time Reversal Symmetry [19000]
- DWF Ensemble from RBC

### Hadron Physics from First Principles [19005]
- Relevant for JLab and Ion-Electron collider
- Physical pion mass
	- Configurations will be available for USQCD
- Variational method w/ good control
- Code readiness is excellent with realistic estimates

### The Elastic Structure of the Nucleon from QCD [19001]
- PI: A. Walker-Loud
- Proposal has a clear goal (compute a single number @ end of calculation)
- Disappointed:
	- Have measured this quantity on different models but fail to convince us that this is worth computing again
- They are confident in their proposal
- Choice of action is questionable
- Bring errors down from 10% to 5%
- Also working on computing these quantities at Livermore

### Real-time dynamics of superfluid nuclear systems [19002]
- PI: Aurel Bulgac
- Nuclear physics proposal
	- proton and nucleon number for both even and odd cases
	- reactions useful for creating heavy nuclei
	- ML for PDEs
		- justified?
	- Qualified team with solid track record
		- **Publish their code**
		- impact beyond nuclear physics (MCNP, MCPNx)
- Large resource request

### Nuclear Femtography: Parton Distribution Functions for the Electron-Ion Collider [19006]
- First reviewer (Marcel Demarteau):
	- Milestones are vague, proposal is nearly identical to the 1-year proposal from last year
	- Want to reduce uncertainties to 5% (why?)
	- HMC production code not ready
- Second Reviewer (Sinéad Ryan):
	- Have exceeded milestones from last years proposal
	- Not surprising there are no publications yet
	- Strong support on computational side, confident in proposals ability
- Some reservation about proposal only using lowest modes
	- Novel approach but unknown whether or not it will allow them to hit their proposed uncertainties
- What is their error budget in terms of systematic uncertainties?
- LOTS of online storage
- Code requirements are the same, `chroma`, `QUDA`
	- Robert Edwards (Chroma)
	- Balint (Chroma --> Frontier)
	- Frank Winters (working on JIT compilation)
- Does it make sense to duplicate computations??
	- Very similar to Jlab proposal
		- Is it wasteful to duplicate configuration generation on different parameter sets?
- Some reservations:
	- Not using state of the art approach
	- Code not ready yet

### Precision Calculations of Matrix Elements for Novel CP Violation Experiments [19007]
- Solid proposal
- No reservations that the team will be able to accomplish this
	- Team has delivered on previous INCITE proposals
	- Timely and

### Gravitational Form Factors of the Nucleon and Pion [19008]
- 1 year project on Summit
	- part of a wider project
- Going to use overlap fermions, mixed action
- Chiral fermions make some extrapoltions easier
- Estimation ~ O(a) improved
- Dirac is normal
- Need to port their chroma extensions
- 6 / 12 months will be spent porting to QUDA
	- Potentially worry-some?
	- Some reservations
- Fill in some gaps in previous extrapolations

### Ab-initio Nuclear Structure and Nuclear Reactions [19009]
- New proposal
	- "umbrella" grants discouraged ?
		- Haven't stopped previous proposals from this group
- Large node hour requests
- Well funded in previous requests
- Many different calculations and directions included
- $0\nu\beta\beta$ neutrinoless beta decay
- QMC Equation of State
	- Green's function Monte Carlo methods
- 2 and 3 body interaction terms
- Good benchmarking, good experience, they've done this before, no reason to doubt their ability to execute

### Insights on Proton Structure and Nuclear Reactions [19010]
- Possibly smaller impact than other proposal
- (had to step out briefly)

### Heavy Quarks in the QGP: Inputs for sPHENIX and LHC [19011]
- hot QCD collab
- areas:
	- quarkonium mass in QGP
	- real and imaginary parts of QQ potential
	- thermal diffusion in the QGP
- Use gradient flow to control signal to noise
- Not aiming at high precision
- Simulations w/ low node counts
- Critical slowing down at (1/a) = 6.2 GeV ?
- Well motivated physics

### QCD Under Extreme Conditions [19003]
- Reservations about Complex Langevin
- Lattice artifacts resulting from staggered fermions
- Axion phenomenology / interactions / nuclear equation of state
- Moments of < Q >
	- Strageness fluctuations
- Analytical continuations --> QCD Phase Diagram

### Advances in Quark and Lepton Flavor Physics with Lattice QCD [19004]
- 3 year request
- (g - 2) HVP using HISQ & DWF
	- HISQ @ Physical point:w
	- International effort to reach consensus and resolve discrepancy
- 3 main topics:
	- (g - 2):
		- anomalous magnetic moment of muon via hadronic vacuum polarization (HVP)
		- Using HISQ & domain wall fermions (DWF)
		- HISQ @ Physical point
	- Existing discrepancy w/ BMW
		- Need to control systematics
	- B, D meson physics
		- Scalar, vector form factors for EW / CKM
	- Indirect CP violation in kaon decays
		- Computing ε_k, δ_M_K
- Previously awarded INCITE proposals
	- Strong team