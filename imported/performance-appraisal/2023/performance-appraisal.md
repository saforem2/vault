````col
```col-md
flexGrow=2
===
```
```col-md
flexGrow=1
===
$\hspace{20pt}$
```
```col-md
flexGrow=1
===
<span style="text-align: right; color:#838383; font-size:0.9em; margin-bottom: 0em; margin-inline-end: 0em;"> Sam Foreman, 2023</span>
```
````
# `rir:UserStar` Statement of Accomplishments
## `rir:Newspaper` Publications

- [GenSLMs: Genome-scale language models reveal SARS-CoV-2 evolutionary dynamics](https://www.biorxiv.org/content/10.1101/2022.10.10.511571v1.abstract)
  - <span style="color:#FFC100">`fas:Trophy`</span> [ACM Gordon Bell Special Prize for HPC-Based COVID-19 Research](https://www.acm.org/media-center/2022/november/gordon-bell-special-prize-covid-research-2022)  
  > <span style="font-size=0.9">"Thanks to your efforts, the “GenSLMs: Genome-Scale Language Models Reveal SARS-CoV-2 Evolutionary Dynamics” project proved the great potential of using high performance computers to analyze large-scale biological data. It is impressive science that will have far-reaching impacts."<br></span>
  > – Paul Kearns
  
- [MLMC: Machine Learning Monte Carlo for Lattice Gauge Theory](https://indico.fnal.gov/event/57249/contributions/271305/)[^1]

- Intro to HPC Bootcamp: Engaging New Communities through Energy Justice Projects[^2]
	- [Exploratory Analysis of Climate Data with ClimRR](https://saforem2.github.io/climate-analysis), Intro to HPC Bootcamp @ NERSC
 
- Performance Evaluation of Large Language Models on Diverse AI Accelerators[^3]

[^1]: To be published in Lattice 2023 Proceedings
[^2]: Submitted to: Tenth SC Workshop on Best Practices for HPC Training and Education at SC23
[^3]: Draft in-progress

## `rir:Slideshow` Presentations[^invite]

- [Scaling LLMs for Science and Ongoing Collaborations](https://saforem2.github.io/scaling4science/), at [_Data-Intensive Computing and AI/ML Applications at Scale_](https://events.cels.anl.gov/event/426/overview), August 2023

- [MLMC: Machine Learning Monte Carlo](https://saforem2.github.io/lattice23), at [_Lattice 2023_](https://mlmc2022.github.io/), July 2023

- [Generative Modeling and Smarter Sampling for Lattice Gauge Theories](https://saforem2.github.io/lqcd-pasc23/), at [_PASC23_](https://pasc23.pasc-conference.org/), July 2023

- [Efficient Sampling Techniques for Lattice Gauge Theory](https://saforem2.github.io/deep-fridays), at [_Deep Fridays @ U. Bologna_](https://www.cs.unibo.it/~asperti/deep_fridays.html), April 2023

- [Large Scale Training](https://saforem2.github.io/ai4sci-large-scale-training), at [_Introduction to AI-driven Science on Supercomputers: A Student Training Series_](https://github.com/argonne-lcf/ai-science-training-series), November 2022

- [Hyperparameter Management](https://saforem2.github.io/hparam-management-sdl2022), at [_2022 ALCF Simulation, Data, and Learning Workshop_](https://www.alcf.anl.gov/events/2022-alcf-simulation-data-and-learning-workshop), October 2022

[^invite]: "_We would like to invite you to speak about your work on ML for gauge field generation at the upcoming workshop "Machine learning for lattice field theory and beyond", which will take place June 26-30, 2023, at ECT* in Trento, Italy_", unfortunately had to decline due to conflict with PASC23

## `rir:Building` Organizational Efforts

- Served as chair / convener for [Algorithms and Artificial Intelligence](https://indico.fnal.gov/event/57249/sessions/22870/#20230731) parallel session at Lattice 2023

- Organizer for [Machine Learning and Quantum Computing for Earth Sciences](https://17.usnccm.org/702) at 17th U. S. National Congress on Computational Mechanics, July 2023

- Organizer for [SC23 Workshop: High Performance Python for Science at Scale (HPPSS)](https://hppss.github.io/SC23/), November 2023

## `rir:Flask` Scientific / Technical Achievements

### `rir:Microsoft` DeepSpeed4Science[^ds4sci]

> _**Enabling Large-Scale Scientific Discovery through Sophisticated AI System Technologies**_

- Ongoing collaboration between ALCF and DeepSpeed team from Microsoft as part of [DeepSpeed4Science](https://deepspeed4science.ai) project
- Microsoft blog post: [**DeepSpeed4Science Enables Very-Long Sequence Support via both Systematic and Algorithmic Approaches for Genome-scale Foundation Models**](https://deepspeed4science.ai/2023/09/18/model-showcase-genslms/)
- Part of this effort has been focused on enabling long sequence lengths for training [`rir:Github` `GenSLM` models](https://github.com/ramanathanlab/genslm)
    - **This will allow us to build foundation models trained on significantly larger genomes than previously achievable**
- `rir:Github` [`microsoft/Megatron-DeepSpeed/deepspeed4science`](https://github.com/microsoft/Megatron-DeepSpeed/tree/main/examples_deepspeed/deepspeed4science/megatron_long_seq_support)
    - `rir:GitBranch` `rir:Github` [`argonne-lcf/Megatron-DeepSpeed`](https://github.com/argonne-lcf/Megatron-DeepSpeed)
- `rir:Github` [`ramanathanlab/GenSLM`](https://github.com/ramanathanlab/genslm)
	- [_Loooooooong Sequence Lengths_](https://github.com/ramanathanlab/genslm/tree/main/examples/long-sequences#loooooooong-sequence-lengths)

[^ds4sci]: https://deepspeed4science.ai
   
### `rir:Earth` Climate Modeling

- `rir:Github` [`argonne-lcf/cnn-esm`](https://github.com/argonne-lcf/cnn-esm)
- Ongoing collaboration between climate modeling team (Rao Kotamarthi, Troy Arcomano, Romit Maulik, Bethany Lusch, Venkatram Vishwanath) and DeepSpeed team from Microsoft to train a foundation model for climate modeling
    - <span style="color:#FFC100">`fas:Trophy`</span> Impact Argonne Award for **Innovation** for:
        - Developing an AI model for climate and creating an innovated data assimilation methodology, positioning Argonne as a global leader in this transformative technology.

### `fas:Dragon` [HPE Dragon](https://dragonhpc.github.io/dragon/doc/_build/html/index.html)

- Ongoing collaboration with HPE (Pete Mendygral) to test / provide feedback for Dragon library from HPE
- `rir:Github` [`DragonHPC/dragon`](https://github.com/dragonhpc/dragon)
    - Dragon is a composable distributed run-time for managing dynamic processes, memory, and data at scale through high-performance communication objects. Some of the key use cases for Dragon include distributed applications and workflows for analytics, HPC, and converged HPC/AI.

### `rir:Cloud` IBM Climate Portal

- Sponsored research collaboration (CRADA) between ALCF and IBM to develop a web-based data portal (frontend) to interface with historical climate data on ALCF filesystems


### `rir:Artboard2` [Lattice QCD](https://saforem2.github.io/l2hmc-qcd)

 - `rir:Github` [`saforem2/l2hmc-qcd`](https://github.com/saforem2/l2hmc-qcd)
 	- End-to-end framework for training and evaluating generative models for Lattice QCD.
 	- Scalable, well-maintained codebase w/ support for:
        - TensorFlow + `Horovod`
 		- PyTorch + `{DDP, DeepSpeed, Horovod}`
- `rir:Slideshow` Talks:
	- [MLMC: Machine Learning for Monte Carlo](https://saforem2.github.io/lattice23), at [Lattice 2023](https://mlmc2022.github.io/), July 2023
	- [Generative Modeling and Efficient Sampling](https://saforem2.github.io/lqcd-pasc23/) at [PASC23](https://pasc23.pasc-conference.org/), July 2023
	- [Efficient Sampling for Lattice Gauge Theory](https://saforem2.github.io/deep-fridays), at [Deep Fridays @ U. Bologna](https://www.cs.unibo.it/~asperti/deep_fridays.html) April 2023

- `rir:Group2` Projects:
	- Member of the [_USQCD Collaboration_](https://www.usqcd.org/)
	- Ongoing work (through 09/2023) for the `l2hmc-qcd` project with James Osborn[^ANL] and Xiao-Yong Jin[^ANL]
	- Ongoing collaboration with the _Critical Slowing Down_ sub-group of the LatticeQCD ECP[^ECP]:

[^ECP]:
      > Xiao-Yong Jin[^ANL], James Osborn[^ANL], Peter Boyle[^BNL][^edb] , Chulwoo Jung[^BNL], Yong-Chull Jang[^BNL], Taku Izubuchi[^BNL][^RIKEN], Norman Christ[^columbia], Richard Brower[^boston], Carleton E. Detar[^utah], Andreas S Kronfeld[^FNAL], Akio Tomiya[^RIKEN,BNL], Luchang Jin[^conn]
[^ANL]: Argonne National Laboratory
[^BNL]: Brookhaven National Laboratory
[^edb]: The University of Edinburgh
[^RIKEN]: Institute of Physical and Chemical Research (RIKEN)
[^columbia]: Columbia University
[^boston]: Boston University
[^utah]: University of Utah
[^FNAL]: Fermi National Accelerator Laboratory (Fermilab)
[^conn]: University of Connecticut

### `fas:ChalkboardTeacher` [Intro to HPC Bootcamp](https://shinstitute.org/intro-to-hpc-bootcamp/)

> An immersive[^immersive] program designed to provide students in STEM with hands-on experience working on energy justice projects using state-of-the-art computational and data science tools and techniques

- [NERSC/intro-HPC-bootcamp-2023](https://github.com/NERSC/intro-HPC-bootcamp-2023?tab=readme-ov-file)
    - Served as project lead for ["Energy Justice Analysis of Climate Data"](https://shinstitute.org/energy-justice-analysis-of-climate-data/)
- [Intro to HPC: ClimRR](https://saforem2.github.io/climate-analysis/)
    - Wrote / prepared material introducing students to geospatial data analysis using data from the [Climate Risk \& Resilience Portal (ClimRR)](https://disgeoportal.egs.anl.gov/ClimRR/)

[^immersive]: Week-long, in person Bootcamp at [Berkeley Lab](https://www.lbl.gov/)
## `rir:Braces` Contributions to ALCF

- Ongoing efforts with Intel towards benchmarking and optimizing LLMs on ALCF systems in preparation for Aurora
- Served as mentor (`ImLab`) at ALCF INCITE Hackathon
    - Helped team to modify their code to be compatible with multi-GPU distributed training
    - Following my suggestions, the team was able to successfully scale to >128 Nodes on Polaris
    - Resulted in a new collaboration and ongoing projects with Haky Im[^uchicago] (and team)
        - Currently writing up recent Enformer results for upcoming publication
- Helped organize / prepare material for [Introduction to AI-Driven Science on Supercomputers: A Student Training Series](https://github.com/argonne-lcf/ai-science-training-series) @ ALCF
    - Wrote material for + gave presentation on [Large Scale Training](https://saforem2.github.io/ai4sci-large-scale-training)
- Helped organize / prepare material for [2022 ALCF Simulation, Data, and Learning Workshop](https://www.alcf.anl.gov/events/2022-alcf-simulation-data-and-learning-workshop)
    - Wrote material for + gave presentation on [Hyperparameter Management](https://saforem2.github.io/hparam-management-sdl2022)
- Submitted proposal on "_Quantifying and Propagating Model and Data Uncertainties in Complex Systems_" (with collaborators from Emory, GMU, NCSU, and ANL)
- Submitted proposal on "_Subsurface Energy Twin – A Digital Twin for Flexible Subsurface Energy Extraction and Storage_" (with collaborators from University of Houston (PI), UT-BEG, PNNL, LBL, Nvidia, and Fervo Energy)
- Interviewed several postdoc and staff candidates
- Gave Presentation on [Scaling LLMs for Science and Ongoing Collaborations](https://saforem2.github.io/scaling4science/) at [Data-Intensive Computing and AI/ML Applications at Scale](https://events.cels.anl.gov/event/426/overview) (08/17/2023)
- Served as 2023 INCITE Computational Readiness Reviewer
- Contributed to MLPerf-HPC Submission on Polaris
- Ongoing work to build / deploy different MLOps tools and services at ALCF
- Contributed to:
    - `rir:Github` [`argonne-lcf/Megatron-DeepSpeed`](https://github.com/argonne-lcf/Megatron-DeepSpeed)
    - `rir:Github` [`argonne-lcf/user-guides`](https://github.com/argonne-lcf/user-guides)
    - `rir:Github` [`argonne-lcf/gettingStarted`](https://github.com/argonne-lcf/gettingStarted)
    - `rir:Github` [`argonne-lcf/ai-science-training-series`](https://github.com/argonne-lcf/ai-science-training-series)

[^uchicago]: University of Chicago

## `rir:Calendar` Goals for Next Year (2024)

- [ ] Continue to build collaborations outside of my domain of expertise
- [ ] Meaningfully contribute to division(/lab)-wide efforts
    - [ ] Continue to pursue additional outreach / educational / DEIA efforts
- [ ] Help to further simplify onboarding process for new facility / machine users (esp. as Aurora begins to enter production)
    - [ ] Continue to write / improve documentation and provide examples / tools to simplify users' workflows
- [ ] Meaningfully contribute to Trillion Parameter Consortium effort
- [ ] Push on workflow development and tools for data services (e.g. model serving, MLOps, etc.)
## `rir:CalendarCheck` Goals from Last Year (2023)

1. Continue building cross-domain collaborations and meaningfully contribute to science projects outside my current focus (Lattice QCD)
    - [x] In the past year I have contributed to:
        - `ris:Microsoft` Ongoing [DeepSpeed4Science](#`rir%20Microsoft`%20DeepSpeed4Science[%20ds4sci]) collaboration with Microsoft[^ds4sci]
        - Two different computational biology projects ([GenSLM](https://www.biorxiv.org/content/10.1101/2022.10.10.511571v2) and ImLab's `enformer` implementation)
        - [Climate Modeling](#`rir%20Earth`%20Climate%20Modeling) project
        - _Geothermal and Long Duration Energy Storage Earthshot_ project
        	- Last year (2022) as a mentor for the `ML4GEO` Team at Nvidia GPU-Hackathon 
        		- Went on to submit proposal (2023) on _Subsurface Energy Twin – a Digital Twin for Flexible Subsurface Energy Extraction and Storage_
        		- Ended up co-organizing [workshop](https://17.usnccm.org/702) at USNCCM 2023
1. Continue to lead discussions and coordinate efforts within the data science and ALCF-Workshop groups
    - [x] Organizer / Project Leader for [Intro to HPC Bootcamp](https://shinstitute.org/intro-to-hpc-bootcamp/)[^hpcb]
    - [x] Helped organize and contributed to [Intro to AI-Driven Science on Supercomputers: A Student Training Series](https://www.alcf.anl.gov/alcf-ai-science-training-series)
2. I'd like to continue mentoring student(s) and keep up / expand my involvement in "student related" lecture series / workshops / outreach events
    - [x] [ALCF summer students gain hands-on experience with high performance computing](https://www.alcf.anl.gov/news/alcf-summer-students-gain-hands-experience-high-performance-computing)[^quote]
    - [x] Supported summer intern who has been working on building out a library to help profile and benchmark NCCL collective communication in ML applications
    - [x] Participated in [Sustainable Research Pathways Matching Workshop](https://shinstitute.org/sustainable-research-pathways-2024-workshop/), a workforce development program designed to connect students and faculty working with underrepresented groups*
    - [x] Serving as mentor for newly-appointed postdoc
    - [/] Approached by student to sponsor [Schmidt AI in Science Postdoctoral Fellowship](https://aiscience.uchicago.edu/) Application

[^hpcb]: The Intro to HPC Bootcamp is inspired by the [Department of Energy](https://www.energy.gov/) (DOE) [Office of Economic Impact and Diversity](https://www.energy.gov/diversity/office-economic-impact-and-diversity) (ED) [Justice40 Initiative](https://www.energy.gov/diversity/justice40-initiative) and makes use of some of the initiative’s resources.

[^quote]:
    > I will note the original draft had a quote that was very complementary of his experience working with you :)
    > > "_Negash wishes to express 'heartfelt gratitude to my mentor Sam Foreman, who did not tire from answering my questions and who made it his focus to teach me in every way he could throughout my time at Argonne_'".
    >
    > – Jim Collins


[^climate-award]: For which I was awarded an <span style="color:#FFC100">`fas:Trophy`</span> Impact Argonne Award for **Innovation**
