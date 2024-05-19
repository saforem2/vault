---
date created: Wednesday, September 21st 2022, 7:38:30 am
date modified: Wednesday, September 21st 2022, 6:02:11 pm
title: INCITE 2023

---

# INCITE 2023

## Engineering 1

- [Link to proposals](file:///Users/saforem2/work/INCITE-2023/Engineering-1)
- General comment:
	- In the regime of highly resolved but not exactly right simulations:
		- get details exactly right or
		- get a better physical description

## Cavitation Inception in Turbulent Liquid Metal

- Kevin Clarno (UTexas): **10**
	- ORNL Proposal
	- General atomics
	- High power densities in small regions
	- Failed welds and cavitation
	- Code has been run on Summit
	- Broken problem down into several distinct phases
	- Clear understanding of needs, node hours required, etc
	- Once cavitation is understood, plan to focus on the effect of the pressure wave from the pulse.
	- Proposal stood out in level of detail
	- Confident in teams ability to perform analysis
- John Turner: **9**
	- Liked the fact that its addressing a major challenge at a major DOE facility
	- Using one user facility to advance another user facility is good for DOE
	- Applications for both fission and fusion technologies
	- Wasn't clear if code was user for fluids other than water (liquid metals?)
- Gorazd Medic **5**:
	- Some question about whether the models will be able to capture the physics
	- More exploratory in terms of approach (for this particular case)
		- Multiple pressure waves through liquid mercury

## Toward In-Service Realism: DNS of Gas Turbine Blades with Localized Roughness

- Clarno: **8**
	- 1 year, Summit / Frontier
	- Similar to Moin proposal (ice effects)
	- Impact on blade lifetime
	- Good scaling studies, looks strong but unfamiliar with code
	- Strong team
- Suresh Menon: **10**
	- Good team
	- Well published work
	- Went through analysis of cost, post processing plans, well thought out
	- Have not demonstrated
- Sibendu Som: **8**
	- Agreement with what was previously mentioned
	- Code written in Fortran
	- No mention of post analysis
	- Not much mention on viz.
	- Highest rated
	- Details about data management plan missing
	- Concern about readiness on Frontier

## High-Fidelity Turbulence Simulation of Three-Dimensional Complex Flow Separation

- Gorazd Medic: **7**
	- Liked the most in terms of technical content
	- Entirely about trying to a DNS of a 3D separation over bump at high Res
		- 160b points
		- past attempts were low res or simplified physics geometry
	- Flows with DNS like this have not been documented much
	- Narrow impact
		- Not many need / care about it from an impact standpoint
	- can be used to calibrate lower fidelity models, but a very specific field
	- well articulated
	- build up by progressing from coarse --> fine grid
- Suresh: **8**
	- Clear funded project from nasa and naval reactors because bumps are important
- Ray: **7**
	- Weakness for well-coordinated community campaigns
	- Fundamental turbulence that is long studied
	- Need is persisntent
	- Concerns:
		- Resolution
			- Not sure this is DNS
		- 4th order code trying to compete with spectral is a handwave
	- Elis method for LES
	- For benchmark data, you have to know where your physics is wrong and using Eiles is closely coupled to BCs and it might not be right in some areas
	- Have been doing this a long time
	- Interested in transonic and supersonic, but comparing with low-speed experiments

## Novel High-Fidelity Moment Closures for Polydisperse Multiphase Turbulent Flows

- Som: **7**
	- 1yr, 1M hrs on Theta
	- Moment based methods for polydisperse
	- First of its kind, interesting approach
	- if successful would be significant
	- Building upon
	- Well articulated
	- Mention using Globus
	- Have had a DD before @ ALCF
		- Used to estimate Milestone 1 (--> Milestone 2)
		- Milestone 3 focused on analysis
	- Need to model vaporization but this is not discussed in the proposal
		- Especially for higher order moment methods
	- Overall clear publication record
	- Have published in excellent journals
- Suresh Menon: **7**
	- Source terms not well defined
	- Concerns about being able to validate results
	- Concerns about physics
	- No storage requirement??
		- No plans to share or even access data (no offline storage) ?
- Samir Rida: **6**
	- Liked the proposal
	- Two (related) goals (that could have been split into 2 proposals):
		1. Using PGMs to better understand the accuracy of aerosol dispersion
			- Moment based method for dispersion
			- Other methods are not
		2. Non-continuum effects
	- Milestones are well defined for each category
	- Project would first need to tackle PGM model for aerosol dispersion
	- Milestone 1:
		- Mention that their model does not account for turbulence
		- Performance tuning
		- Outcome important for next milestone

## Direct Numerical Simulation of Aerospace Combustion with Sustainable Aviation Fuels

- Excellent team w/ previous INCITES
- Code is ready
- gas turbine combustors
	- important stabilization is:
		- counterflow
		- recirculation zones
		- swirl stabilization
- Some risk on the modeling side
- Risk in year 1 may impact / risk following years
- Physics of the stabilization isn't really there in this one
- Other one has more relevant geometry

## First Principles Simulation of Hypersonic Flight

- Rankings:
	- Anil: **9**
	- Flavio: **9**
	- Samir: **7**
- Focus on hypersonic flow past realistic obstacles
- Demands the use of direct molecule simulations (DMS)
	- Molecular dynamics using potential energy surfaces using NNs
	- Articulated explicit pairs which will interact in air
- Work is of high value and approach can be used in wider applications
- One of a kind in this field
- Proposed a novel approach to eliminate the phenomenological assumptions of other MCMC simulations
- Provide high quality assumption free result
- Others can use results from this study to calibrate lower order models
	- Will drive further improvement
- Developed in a systematic way how to gradually increase complexity and gives them predictive power in their approach
- Computational approach is well described in the proposal
	- Nicely presented
- High likelihood of relevant conclusion
- Uses appropriate algorithms and data analysis
- High fidelity experiments which measure the partition energy sdistribution and will be able to compare against their code
	- big step in validating this approach
- Good use of machines
- Unclear about node hour request:
	- mismatch between request for years 1 and 2 ? (page 9)
	- Asking for two years worth of time on Theta?
	- Mark said it will be looked into and followed up on
- Sparta DMS leveraging ??? infrastructure
- Authors were awarded 2022 INCITE to run similar calculations of experimental conditions
	- Is this proposal an extension? unclear
	- Methods proposed have already been studied in previous grants ?
- Needs to be clearly defined how development work impacts the work they proposed
- Mentioned that they would need to use CPU-GPU in year 2-3,
	- under development section mentioned code would be ported to GPU
	- Reasonable justification for petascale computing needs

## A Multiphysics Approach for Guided Human-Scale Mars Lander Descent Simulations

- Samir Rida: **9**
	- Continuation of 2022 INCITE Plan ?
	- Simulation of full 6 degree of free
	- Mach 2.4 to 8
	- 30 second simulation
	- Connection with the reaction control system
	- Prepared to leverage exascale computingA
	- Not entirely original, but of high value
	- Will require large scale computation
	- No experimental approach to obtain these results / data
		- not achievable in wind tunnel
	- Optimized simulation trajectories using Post2 and Fun3d
		- fun3d used on Summit
		- validation on Nvidia GPUs
	- Work been done to get ready for Frontier
		- Work has been done on Crusher
		- achieved noticeable speedup compared to V100
	- Elaborated on robustness of ITAR
	- Claim that remote connection will not impact the performance
	- In order to meet objectives, authors propose 3 tasks in 1 year
	- 10 species, 1.5b grid with 5 dof --> 6 dof with full engine and control
	- milestones well defined, good detail, no need for archival storage
		- Visualization to be performed on summit
	- Team is well qualified
		- Working on project with 2022 INCITE
	- Ready for Frontier in 2023 on track
	- Switch from Nvidia --> AMD seems to be on track as well
	- Reasonable node hours requested for task
		- Revised down from last year
- Kevin Clarno (UTexas): **8**
	- Very strong proposal
	- Reasonable allocation request
	- Unclear how to validate simulations
	- Capable of getting simulations done and expect they should be successful whe
- Suresh Menon: **9**

## The First Full-Resolution Liquid-Gas Disperse Flow Simulations

- Ray Grout: **7**
	- Simulating bubbly flow
	- Point to a problem related to caviation flows and mass transport betwen the phases
	- Two thrusts
	- Plan to build very detailed data sets
	- compressible forumation, shock capturing
	- On balance, reasonable request
		- 500K Summit
		- 4.5M Summit equivalent on Frontier
		- 1M Node hours on Frontier (native hours)
		- Large but not unusually large request
	- Approach is rigorous, scientifically sound
	- Broadly relevant output
- Anil: **7**
	- Aligned with previous comments
	- does not like flat grid
	- impressed by approach
	- leveraging shock capturing to capture interface between phases
	- Good detail in calculating resource request
- Kevin: **6**
	- Unique in trying to resolve things at the proposed scale
	- Not clear how it will impact additional scientific fields
	- Extensible?
	- Would other media need more calculations for developing the sub-grid scale models?
	- Not clear that this is the correct long-term approach
	- Mixed grid
	- Parallel performance looks good
	- Low rating bc of massive compute requested, seems to outweigh scientific impact

## Full-Core RANS-LES at Exascale: Breaching the Billion Spectral Element Mark

- Kevin: **8**
	- Every year increase the size and scale of problems they plan to look at
	- Long term plans, this proposal is the logical next step in the process
	- Flow drives a lot of the physics for reactors, nuclear safety
	- Very important, significant physics problem they plan to address
	- Software and team are strong, with good scientific proposal
	- lots of discussion on model setup
	- little discussion on how the generated data will be used
	- impact on pressure drops
		- temperature distribution
	- How to go from generating high resolution models of the flow in the core to answering the questions?
		- Not even addressed
	- Plan to do full core with 6-9 assemblies
	- If done well in great detail, could produce low order models to be used in safety codes
	- Not clear even for simulations being done now how the data will be used / analyzed
	- Milestones
	- Not much detail on what they're going to be comparing
		- Which lower-fidelity codes to be used
		- Didn't go into detail for how data was going to be used to answer those key questions
	- Maybe a bit oversold
- Gorazd: **5**
	- Effectively a continuation of 2022 INCITE Project
	- Not clear why it isn't a renewal
	- Main driver is increased geometric complexity
	- Worried about validation
	- Not clear how more geometric complexity will improve results
	- Not too excited about this one
- Medic: **5**
	- Unclear why it isn't a renewal
	- Lack of analysis, description of impact
- Flavio Chuahy: **8**
	- Appear to be extending from RANS to LES
- Feels like a renewal
	- Request 1 year proposals every year
		- Can get away without explaining plans for detailed analysis
	- Should be multi year proposal with additional description + emphasis on analyzing /

## Predictive High-Fidelity Simulations of Aircraft Icing and its Aerodynamics

- Gorazad Medic: **7**
	- Simulations not about icing itself but what happens with roughness of surface
	- uses scans of a surface
	- wallr-esolved models and then will update the wall model in the same code to make it usable
	- program is well defined with focus and planned milestones for each of the three years
	- can be applied to turbomachinery
	- Reluctant because they haven't done this much before
		- Overall liked the proposal
- John Turner: **9**
	- Nothing to add
- Samir: **7**

## Wall-Resolved Large Eddy Simulation of the NASA CRM High-Lift Configuration

- Menon: **8**
	- 2nd year renewal
	- Have used system effectively so far
	- Trouble with the grid:
		- lower order grid with higher order scheme
		- Previous simulation of WRLES were reasonable
		- Comparing CP / CL ?
	- No novelty except is a renewal
	- Would be nice to know why Modeled LES
	- LES itself is implicit
	- Recommended for year two renewal because they're already on the system and have been utilizing it
- Anil: **6**
	- Agree with Suresh
	- Met proposal milestones
	- Issues with grid seem to have been resolved
	- Seem to have a path forward
	- Have taken an approach that may not be the best suited but have been making progress
	- Should continue
- John Turner: **8**
	- Similar observations
	- Had to significantly modify their plan after troubles with mesh
		- Have done this and come up with a new plan
- Much more data produced than measurement, makes it hard for comparison
	- Makes it hard to interpret
- Suresh:
	- More data
- Samir:
	- No real novelty to this approach

## Rankings Notes
- MacArt (15003_Kos):
	- Narrow Scope
	- Same issue as with mars lander
	- Seems highly ranked
	- Can't see broad impact
	- Worried about
- Discussion about 15003_KOs (Cavitation) about Gorazd Medic's score of **5**
- Discussion about how many proposals will be funded
- Gorazd Medic question about 15005_Mac (Extreme-Scale Data) how well the request for resources is justified
- Funding the first one (Roughness) makes the Icing one redundant
- Question about Flow separation & Icing ones being in the right place
	- Icing & Roughness
- Seems tough for reviewers to compare closely ranked proposals
	- Especially for reviewers which only reviewed subset of those being discussed
- Discussion about 15005_Mac (MacArt):
	- suggestion to reduce scope by 50% and pick 2 / 4 of the proposed problems
- Renewals:
	- No objections
	- Good progress
	- Fail to provide explanation and justification for why they can do the Wall model