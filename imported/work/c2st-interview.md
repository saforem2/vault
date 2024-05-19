Solving The Unsolvable With Supercomputers--An Interview With Dr. Sam
Foreman

Argonne National Laboratory is home to several supercomputers with
impressive computational power that drives innovative discoveries in
numerous research fields. With supercomputing on the rise, there is a
need for continued performance capability and efficiency.

\[Picture #1\]

Through a fellowship in the Science Graduate Student Research (SCGSR)
program, Dr. Foreman worked on his thesis on lattice gauge theory at
Argonne. Now, Dr. Sam Foreman is a postdoctoral research associate
working in the data science group at the Leadership Computing Facility
at Argonne National Laboratory. Dr. Foreman has a background in
Engineering Physics and Applied Mathematics that melds into his work
with software development and code writing for machine learning.

I recently tuned in with Dr. Sam Foreman on Zoom to talk about his
research on machine learning to streamline computational processes,
particularly in lattice gauge theory and lattice quantum chromodynamics
(QCD).

**C2ST: You previously mentioned to me that you had the opportunity to
continue working on your thesis project through a fellowship at Argonne.
Can you tell us a bit more about how that has shaped what you are
currently doing?**

**Dr. Foreman:** Continuing from my thesis work, my research currently
involves lattice gauge theory and lattice quantum chromodynamics
(QCD). QCD theory is the theory of strong interaction, essentially
the strong force that binds the nucleus together. You may have heard of
quarks and gluons, which are the building blocks of protons and neutrons
that in turn form the nucleus. This theory is generally analytically
intractable, meaning as of right now there aren't known methods to solve
things analytically. We can't exactly write an equation down and solve
it through pen and paper. But it's more complex than that since over the
last 50 years we are still no better at solving it. However, one way to
get around this problem and to make this theory useful is to simulate it
on computers.

To simulate it on computers, we discretize space (making space into
mathematically discrete forms for easier calculation) onto a lattice. By
making a lattice, or grid, we can basically run simulations such as
lattice QCD. In a broader context,** **it's the numerical component of
the standard model. The standard model of particle physics describes
particle physics and their interactions with each other. Lattice QCD is
the subfield of this broader standard model of high-energy particle
physics.

**C2ST: Can you describe how these models are supposed to work?**

**Dr. Foreman:** For example, a real-world model essentially captures
some of the behaviors we expect to see in the full model. This "toy
model" allows us to simulate these behaviors in a two-dimensional (2D)
scale with x and y, but the full QCD process is four-dimensional (4D):
x, y, and z with time. In a computationally heavy field, simulations can
take months and months to run on even the biggest supercomputers to
generate results. Running the simulation itself is computationally
demanding, so even if it was all working, scaling up to the full model
is a challenge to orchestrate. It's a bit out of reach for the moment.
This is hugely inefficient, so now, I mainly work on different models
from machine learning that can make the computational process more
efficient to benefit the community.

**C2ST: That's where you come into the equation (no pun intended). With
these models in mind, what is your process like? Are you working on the
drawing board or is it a lot of trial and error on the computer while
you're coding?**

**Dr. Foreman: **My day-to-day is more closely aligned to what a
computer programmer does for software development and general coding, as
opposed to what I historically did as a physics major (pen and paper).
However, the benefit of having a Ph.D. in physics and doing math
historically gives you a different perspective on software development
and writing code.

Even generally, developing code for scientific applications is different
from web development. ~~With the nature of web development, more people
are inclined to jump into writing code.~~ Scientific code has a lot more
theory behind it, so it's trickier to jump into. There are lots of
equations that need to be simplified and translated into code. For
instance, if I wanted to calculate a particular quantity, it may depend
on 5 or 6 layered equations that first have to be written out and
translated in an easy-to-follow fashion within the program.

**C2ST: Do you have to use special programs to accommodate scientific
coding?**

**Dr. Foreman:** Hm, a lot of what I currently do is machine learning
(ML) and most ML code development is done in Python. However, there are
a ton of different applications that can be used such as Matlab or
Mathematica.

**C2ST:** **Since much of your time is spent working on code, what are
some of the challenges that you face? **

**Dr. Foreman:** You don't want to have to reinvent the wheel, like
rewriting things that people have already done. But on the other hand,
for my ML learning framework, there wasn't much to go off of (i.e., like
on Google). Since this is a very niche topic, it is uncharted territory
and you kind of feel like you're just winging it. In that same vein
though, the uncertainty is part of the fun of it! I think research would
be boring if everything were a linear path and there wasn't that unknown
factor of "will it or won't it work".

**C2ST: Aside from your research, I see you have been busy with other
extracurriculars! You have been involved with Argonne's Q&A threads on
Twitter. Were you always active on Twitter or did your involvement
change throughout your academic and professional career?**

**Dr. Foreman:** I've been on Twitter since about 2011-2012. It just hit
me how long ago that is because a few weeks ago Twitter sent me a
notification about how it's been 12 years. Back in 2012, I was an
undergrad and I only used Twitter casually until grad school. Once I was
in grad school, I started to realize the value that Twitter had-not even
as a scientific tool, but I thought it was useful in following
interesting people doing interesting things. It was a great way to get
started in exposing myself to these things on my feed and staying
up-to-date. I had never really had plans of being someone on Twitter,
like those influencers you see nowadays since historically I didn't
really tweet original thoughts. Most of my activity on Twitter was
retweeting the work and thoughts of others. But slowly, I started to
gain more and more followers. I didn't think much of it at first, since
I didn't set out to amass a huge following.

**C2ST: What are your thoughts on using Twitter in the current
scientific landscape? I feel that social media platforms can seem
unassuming at times, but can really shake up one's opportunities.**

**Dr. Foreman:** For me, Twitter has evolved into a useful tool for
meeting new people, setting up collaborations, and even serves as
effective networking for jobs. There was a guy that I had known and
followed. He worked at Intel and I had casually retweeted posts of his
here and there. At the end of grad school, I tweeted that I was
completing grad school and would be on the market for a job. He reached
out to me and said that Intel was hiring and that my research was in
line with what they were looking for. They even offered me a job! The
mere idea of coming out of grad school and making a real "adult/big-boy"
job for quantum computing blew my mind. All of this was facilitated
through minimal interactions online! It was definitely a turning point
in my career and general view of Twitter.

Even now as a postdoc, I really started to see more value in having a
presence on Twitter as a tool to share my own research. It also made me
think about how other researchers may share similar feelings and
struggle with sharing their own work. "Are my thoughts of value to
others?" "What can I say that other people would take meaning from and
think it was interesting?" Lately, I have been getting better at
grappling with those feelings. As a scientist, particularly in this
current climate, it is in your best interest to be authentic and show
who you are. It would be a disservice to yourself and others if you
aren't genuine in these interactions. I want my own personality to shine
through, and so far, people have been receptive to it!

\[Picture #1\]

![](Pictures/100000010000043800000438FEAE94CCBF30A089.png){width="6.4917in"
height="6.4917in"}
