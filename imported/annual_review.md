<div style="text-align: right">
    <br>Sam Foreman</br>
    <br>Postdoc, ALCF (ECP)</br>
	<br>08/2020 -- 06/2021</br>
</div>

# Annual Review

## Scientific or Technological Achievements

### Accomplishments

- Extensive development (sole author) on [`l2hmc-qcd`](https://github.com/saforem2/l2hmc-qcd/) a Lattice QCD mini-app focused on using machine learning to improve the efficiency of Hamiltonian Monte Carlo (HMC) sampling techniques for lattice gauge models.
- This approach was shown to significantly reduce the computational effort (~**100x** speedup) required to generate independent configurations on a two-dimensional U(1) lattice gauge theory model.
- Also consistently outperforms HMC across a variety of toy-models for which HMC is known to be inefficient (Gaussian Mixture Models, Neal's Funnel, etc.).
- Designed, built, and tested a novel network architecture (`LeapFrogLayers`) that forms the basis of our generalized (trainable) HMC algorithm.
- Built a database of HMC data to serve as baseline against which to compare our trained model.
- A focused effort into understanding the models’ behavior at a low-level has resulted in a fairly cohesive understanding of the underlying mechanism driving this improvement.
- Regular presentations and interaction with the Critical Slowing Down sub-group of the Lattice QCD ECP Project.
- Helped build and test ML frameworks on Theta / ThetaGPU as a member of the datascience team.
- Wrote the material on _Scaling Deep Learning Applications using Horovod, TensorFlow, PyTorch and PyTorch DDP_ for the 2021 Computational Performance Workshop.
- Wrote the material on _Hyperparameter search using DeepHyper on Theta_ for the 2020 ALCF: Simulation, Data, and Learning Workshop for AI.
- Lead the discussion on _Switch Transformers_ ([**slides**](https://anl.box.com/v/switch-transformers)) for datascience journal club.
- Regular meetings and interaction with Field Transformations for Lattice QCD group
- Extensive development (main author) of the [`fthmc`](https://github.com/nftqcd/fthmc/) software designed for performing _Field Transformation HMC_.
  - Can be easily trained on a small lattice volume and transferred to a larger volume with minimal retraining effort required.
  - Plan to present this work at the 2021 Lattice Conference (July, 2021).
- Helped contribute to the [_#Exascale_](https://twitter.com/search?q=%23exascale&src=typed_query&f=live) Twitter chat.

### Publications

- Accepted contribution on [_Deep Learning Hamiltonian Monte Carlo_](https://arxiv.org/abs/2105.03418) to the [Deep Learning for Simulation Workshop](https://simdl.github.io/overview/) at ICLR 2021.
  - [poster](https://simdl.github.io/posters/57-supp_DLHMC_Foreman_SimDL-ICLR2021_poster1.pdf)
  - [`github`](https://github.com/saforem2/l2hmc-qcd/)
- Submitted two abstracts to [The 38th International Symposium on Lattice Field Theory](https://indico.cern.ch/event/1006302/).
  - [_LeapFrogLayers: A Trainable Framework for Effective Topological Sampling_](https://indico.cern.ch/event/1006302/contributions/4380743/) (in progress)
  - [_HMC with Normalizing Flows_](https://indico.cern.ch/event/1006302/contributions/4380643/) (in progress)
- Submitted [_Machine Learning and Neural Networks for Field Theory_](https://www.snowmass21.org/docs/files/summaries/CompF/SNOWMASS21-CompF3_CompF2_Sam_Foreman_(V2)-131.pdf) to [SnowMass 2021](https://snowmass21.org/), the HEP Community Planning Exercise, outlining how the Lattice QCD community stands to benefit from recent developments in machine learning.
- Submitted *Towards Efficient Topological Sampling in Lattice QCD* poster as a Research Highlight Slide (AI-ML applications).
- In the media:
  - [Virtual ALCF Workshop Provides Guidance on Using AI and Supercomputing Tools for Science](https://www.hpcwire.com/off-the-wire/virtual-alcf-workshop-provides-guidance-on-using-ai-and-supercomputing-tools-for-science/ )

### Contributed and Invited Talks

- Invited talk on [`l2hmc-qcd`](https://github.com/saforem2/l2hmc-qcd) to the lattice group seminar at MIT
- Invited talk on [_Deep Learning HMC for Improved Gauge Generation_](https://indico.mitp.uni-mainz.de/event/231/contributions/3424/attachments/2628/2882/MLT-Foreman.pdf) to the [Machine Learning Techniques in Lattice QCD](https://indico.mitp.uni-mainz.de/event/231/overview) workshop at the Mainz Institute for Theoretical Physics, Johannes Gutenberg University
- Invited talk on [_Machine Learning for Lattice QCD_](https://slides.com/samforeman/l2hmc-qcd-93bc0c) at the University of Iowa

- Presented poster on *Deep Learning Hamiltonian Monte Carlo* at the ECP Annual Meeting
- Presentation on [*Hyperparameter Search Using DeepHyper on Theta*](https://github.com/argonne-lcf/sdl_ai_workshop/tree/master/03_distributedHyperOpt/01_BasicHPS) at the [ALCF: Simulation, Data, and Learning Workshop for AI](https://github.com/argonne-lcf/sdl_ai_workshop)
- Presentation on [_Scaling Deep Learning Applications_](https://github.com/argonne-lcf/CompPerfWorkshop-2021/blob/main/05_scaling-DL/README.md) at the the [2021 Computational Performance Workshop](https://github.com/argonne-lcf/CompPerfWorkshop-2021)
  - [recording](https://youtu.be/ESbk-ESLhqk)

## Collaborations

- Ongoing work for the `l2hmc-qcd` project with James Osborn (_CPS_, _LCF_)
  and Xiao-Yong Jin (_CPS_, _LCF_)

- Ongoing collaboration with the _Critical Slowing Down_ sub-group of the
  LatticeQCD ECP

  > Norman Christ (_Columbia U._), Richard Brower (_Boston U._), Carleton E. Detar (_Utah U._), Andreas S Kronfeld (_Fermilab_), Peter Boyle (_BNL_, _Edinburgh U._), Akio Tomiya (_RIKEN_, _BNL_), Luchang Jin (_Connecticut U._), Xiao-Yong Jin (_ANL_, _CPS_), James Osborn (_ANL_, _CPS_), Chulwoo Jung (_BNL_), Yong-Chull Jang (_BNL_)

- Ongoing collaboration with _Field Transformation HMC_ group
  
  > Xiao-Yong Jin (_LCF_, _CPS_), Luchang Jin (_Connecticut U._), Taku Izubuchi (_BNL_, _RIKEN_), James Osborn (_LCF_, _CPS_)
  
- Active member of the datascience group in _ALCF_

- Initiated collaboration for LDRD proposal

  > Xiao-Yong Jin (_LCF_, _CPS_),  Ahmed Attia (_MCS_), Arindam Fadikar (_MCS_), Sandeep Madireddy (_MCS_), Jonathan Ozik (_DIS_), James Osborn (_LCF_, _CPS_)

- Member of the _USQCD Collaboration_

## Performance Focus

### Relative strength as an early career researcher

> In what areas does the Postdoc excel? Address both research and professional skills. Provide examples to illustrate strengths.

#### Research / Technical Skills, Managing Projects

- One of my biggest strengths is being confident in my abilities when confronted with new challenges. I believe that my strong analytic background (math + physics with heavy CS undergrad) has provided me with a broad set of skills that allow me to systematically deconstruct a problem into a set of manageable tasks and to identify potential issues which may arise.
- Being innately curious and passionate about a wide range of topics allows me to identify themes and subtle patterns across seemingly disparate fields and ideas which may not always be readily apparent.
- I deeply enjoy performing data analysis and I believe that having a strong statistical background allows me to extract novel insights from existing data and generate accurate predictions about how I can expect the data to behave in the future.
- I always enjoy learning new things and discovering new information.
  - Because of this, I enjoy keeping up-to-date with new developments in my field and have found this to be tremendously beneficial in my own research.
- Capable of turning ideas into manageable plans and executing them with confidence.
  - I enjoy wrestling with new ideas and approaching complicated problems in a systematic and well thought-out manner.
- I have solid problem-solving skills and a sense of determination that allows me to follow my ideas through to their completion.
- Working at the intersection of math, physics, machine learning, and high performance computing has forced me to adapt quickly while effectively taking in new information, allowing myself to remain oriented in an area whose direction is ever-changing.
  - While at times this rapid development cycle and constant evolution can be challenging, I've found that successfully navigating difficult problems is incredibly rewarding and provides a sense of fufillment.

#### Communication / Mentoring / Leadership Skills

- Though I generally consider myself to be independent and self-motivated, I also deeply enjoy working as part of a team.
  - In my experience, I believe that groups tend to operate at their best when everyone is working under a unified vision with well-defined expectations.
  - I've found this to be especially true when working with individuals whose ideals are generally aligned with my own (e.g. compassion, inclusivity, and opennness to new ideas).
  - I enjoy identifying others' strengths and working in an environment that is able to leverage them effectively.
- I am always willing to help others and provide assistance in any way that I can.
  - In graduate school I deeply enjoyed teaching and found joy in helping students achieve their full potential.
    - As an example, during one of my first semesters I was the head TA of an undergraduate course (Physics II: Introduction to E&M). After the first couple of weeks, I quickly noticed that the existing structure of the discussion sections (students come in and copy down the solutions to problems as I worked through them on the board) was ineffective at teaching the students the material.
    - I was able to convince the professor that students would benefit more from a discussion which was collaborative and group-oriented instead of monotonous and dull.
      - By organizing students into groups and having them collectively struggle through the problems together, students were able to identify the gaps in their knowledge and ultimately better understand the material.
    - Following this, I noticed the overall attendance in these sections began to gradually increase, indicating that the students also seemed to enjoy the new format.
    - I consistently received positive teaching reviews, and found that other professors within the department were generally receptive to this new discussion style.
    - Ultimately, a few other professors chose to adapt this new format and I was deeply appreciative of the systematic change to the undergraduate physics curriculum that I was able to help bring about.
  - I believe that helping others (especially without expecting anything in return) helps to give me a sense of fufillment and provide meaning to my work which is crucial in maintaining my intrinsic motivation.

#### Professional Skills / General Strengths

- I am always looking for new ways to challenge myself and tend to actively seek out opportunities that are impactful and have the potential to make a real difference.
  - I would strongly prefer to use my strengths for the greater good than for personal benefit.
  - Bonus points if it is something that pushes me outside of my comfort zone.
- I consider myself to be highly motivated, unfailingly honest and incredibly reliable. Additionally, I think that I am generally open-minded and perceptive to others' ideas and inputs.
  - I think that this set of qualities helps to foster relationships built on trust and integrity.
- General strengths:
  - **Passionate**, **observant**, **idealistic**, **resourceful**, **enthusiastic**
  - Confident in my public speaking abilities and writing skills.
  - Incredibly detail oriented and strive to always do the best I can, never choosing to settle for "good enough"

## Development Focus

### Potential growth and plans for professional development

> What are some key skills to focus on over the next year? What are the opportunities for development? If entering the third year, what will be most beneficial to enabling a smooth career transition?

- I would like to continue developing collaborations with external researchers, especially in areas outside of my current research.
- I believe that mentoring a student would be mutually beneficial, particularly given how much I enjoyed teaching during graduate school.
- Continued development in lower level software + hardware design.
  - While I certainly have experience in this area, I think that continuing to develop these skills will benefit me for the duration of my career.
- For my eventual career transition, I am confident that my skills will provide a variety of opportunities for challenging and rewarding careers, and I look forward to being able to carry with me the skills I've developed here.
