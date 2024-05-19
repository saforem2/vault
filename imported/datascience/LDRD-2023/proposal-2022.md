# pre-Proposal 2023
## Research Opportunity
The application of chemical forensics as a tool for tracing the provenance of chemical-weapons-associated materials is a relatively new and emerging field.

Work in the field is rapidly increasing in intensity and the time for Argonne to assertively enter the field is now to establish ourselves as thought leaders.

In this project, we will develop the chemical forensics methods to identify the provenance of residues associated with chemical weapons activity.

The work will concentrate on taking measurements from field-portable analytical instruments and analyzing them with AI/ML methods to provide practical, rapid provenance information.

To accomplish this, we will combine experimental measurements performed by the Analytical Chemistry Laboratory (ACL) in the CFCT Division (NTNS) with statistical and AI/ML analyses carried out at the Leadership Computing Facility (LCF).

For the experimental work, we will use a field-portable mass spectrometer and a Raman spectrometer, both on hand in the ACL, to measure characteristic signals from contaminants in commercially-procured samples of precursor materials, some of which will be additionally spiked with likely contaminants to generate a larger signature library.

A deep neural network (DNN) will be trained on public datasets, synthetic data, and our collected dataset for identification of provenance-relevant features.

The result will be a unique capability for using inexpensive and portable instruments with sophisticated data analysis to rapidly determine chemical provenance information.

With the results from this work in hand, we will leverage existing connections to the chemical forensics community (through the Chemical Forensics International Working Group and other sources) and to funding sources (including the Department of State, DHS, and DOE-NNSA) to capture additional work and expand Argonne’s presence in this field.


# Proposal 2022
- **LDRD Project Number**: 2022-0052
- **Project Title**: _Chemical Forensics and Signatures for Provenance Tracing_
- **Investigators**:
	- Nicholas Condon (CFC)
	- J. Taylor Childers (LCF)
	- Kristin DeAngeles (CFC)
- **Proposal Summary**:
	- In this project, we will develop the chemical forensics methods to identify the provenance of residues associated with chemical weapons activity. The work will concentrate on the use of field-portable analytical instruments combined with AI/ML methods to provide practical, rapid provenance information. It will leverage existing capabilities to establish Argonne as a thought leader in the field of chemical forensics.

# Research Plan

## Research Goal

The goal of this work is to develop chemical forensics methods using field-portable analytical instruments to identify and detect chemical signatures that serve to identify precursor sources, synthesis methods, and production sites for residues associated with chemical weapons. We will use a field-portable mass spectrometer and a Raman spectrometer (both already on hand in the ACL) to take measurements of the patterns of contaminants in commercially-procured test samples. We will then add spikes of other likely residues and construct a basic library. This library will then be expanded to generate a training set for an AI/ML system. Initially, this would be used to identify fictional production sites based on artificial signature patterns to demonstrate the value of the method. Future work would then concentrate on expanding the training set with the collection of additional data from samples taken in different environments in order to produce a system able to identify the likely sources for a given residue based on its mass spectrum and Raman spectrum.

## Research Opportunity

The application of chemical forensics as a tool for tracing the provenance of chemical-weapons-associated materials is a relatively new and emerging field. Work in the field is rapidly increasing in intensity and the time for Argonne to assertively enter the field is now to establish ourselves as thought leaders. Much of the recent work in this area has used expensive, larger-scale equipment such as isotope ratio mass spectrometers (IRMS)[^1],[^2] to look for isotopic signatures or GC-MS and LC-MS systems to look for chemical signatures[^3][^4][^5]. The capability to use more compact instrumentation would be extremely valuable.

## Research Description

The synthesis, processing, and storage of any organic chemical will leave behind chemical impurities that have the potential to serve as signatures.

Different chemical reaction pathways to a given product are likely to leave behind different residual starting materials (each of which may have their own signatures) and side products.

Post-synthesis processing is expected to remove some of this material (depending on the quality demands and capabilities of the production facility), which will modify the signature in a characteristic way.

Finally, some quantity of the materials may decompose during shipment and storage, and information about the decomposition products may provide information about the history of the sample.

Detection of these signature impurities will be a primary challenge of this work.

Here, we will employ two primary experimental methods: Mass spectrometry and Raman spectroscopy.

For mass spectrometry, we will be using an MX908 Portable Mass Spectrometer.

This is an exceedingly compact, battery-powered, handheld mass spectrometer that was principally designed for use by first responders in identifying chemical substances, including chemical weapons and precursors, in the field.

While its basic operation only produces alarms for specific materials already in its library, the ACL staff have taken advanced training on the device that allows us to download and analyze its raw data, allowing us to use it as a more general-purpose instrument.

It was selected for use on this project, in part, because the portability and small footprint that make it a good choice for first responders also make it an ideal field instrument for chemical forensics work in the field.

Raman spectroscopy will be used to provide complementary data, as its mechanism of detection (based on the frequencies of molecular vibrations) is almost entirely orthogonal to mass spec.

Data for this program will be acquired using the ACL’s existing lab-scale Raman spectrometer.

However, handheld Raman spectrometers with relatively similar performance metrics are now widely available (from companies like Agilent and Bruker), so such an instrument could serve as a field-capable complement to the MX908.

## ML Driven Signal Detection

The application of deep neural networks (DNN) has exploded in the last decade as large-scale computing resources and labeled datasets have become more accessible.

Using convolutional neural networks (CNN) to analyze mass spectroscopy and Raman spectroscopy data has shown great improvements over conventional statistical methods, e.g. Principle Component Analysis (PCA), Partial Least Squares (PLS), Support Vector Machines (SVM).

The literature focuses on properly classifying or identifying the presence of specific substances or complex combinations of substances with early studies using public spectroscopy databases of different Beers, Wines, and Coffees[^6], while examples of more recent studies use DNNs to discern cancerous cells from normal cells[^7] and bacteria classification[^8].

These studies aim to identify signal spectra of target substances in their data, while our goals involve looking for background signals alongside these target substances.

Given a suspect target substance, the mass or Raman spectra will have a distinct signature of the target, but we are also interested in identifying the subtle signatures of leftover constituents and/or possible contaminants that may indicate points of origin.

The example studies above show relatively shallow networks consisting of one or two CNN layers and a fully connected linear feature vector sufficed in reaching leading accuracy (**at classifying the target?**).

We will begin by examining similar networks for our use case.

The existence of public datasets of mass/Raman spectra on which to train such networks can help address another challenge we may face in this proposal, which is a lack of large labeled data to train a DNN.

As an example, the MNIST dataset aims to train for 10 classes and contains 60k 28x28 pixel images, while we will be generating a simulated dataset that will at most consist of order 1000 spectra.

This is likely not enough to properly train a model without overfitting the data, however, one can train the network on a larger public dataset **and use transfer learning to fine-tune the model for our specific use case**.

**This can be done, for example, by freezing all but the final feature layer, allowing the model to learn the unique features of the new dataset.**

~~Then freeze the learning parameters of all but the last feature layer which is allowed to change while training on the target dataset.~~

**Explicitly**, since the spectral features between our dataset and the public datasets are the same, we can re-use the trained CNN layers as they provide the spectral feature extraction, but the last feature layer needs to be tuned to our specific task of recognizing our specific substances.

Our initial experimental work will focus on analyzing commercially-available materials that can also be used in the production of chemical weapons.

These will be drawn from the Australia Group Common Control List Handbook: _Volume 1: Chemical Weapons-Related Common Control Lists[^9]_.

The Australia Group is an informal group of nations that seeks to harmonize export controls so as to counter the proliferation of chemical and biological weapons, so their control lists serve as an excellent compilation of materials of concern for forensics work.

We will acquire samples of several target materials drawn from this list from multiple commercial sources, then analyze them via mass spec and Raman.

We will look for any signs of impurities in the data and attempt to identify them.

The data for a given material will be compared across sources, and the identification of consistent, observable differences between them will constitute fulfillment of our Renewal Milestone.

When possible, observed impurity materials will be obtained and spiked into the target samples for additional measurements.

Continuing experimental work will expand the range of materials that can be analyzed.

Once sufficient data has been acquired, the DNN will be tested against both synthetic data and against real data acquired from fresh batches of material acquired from the sources of interest.

The results of these tests will constitute the final milestone.

**Final Milestone:** Demonstrate the use of an AI/ML system to identify the provenance of test chemical samples based on their mass spectra and Raman spectra.

**Renewal Milestone:** Demonstrate observable differences in mass spectra and/or Raman spectra between test materials from different manufacturers.

# Researcher Roles

Nicholas Condon, as Lead PI, will dedicate about 15% of his time to the project. He will lead the experimental effort and will take primary responsibility for reporting and overall project management.

Taylor Childers, as Co-PI, will dedicate about 10% of his time to the project. He will lead the AI/ML effort.

Kristin DeAngeles, as a Researcher, will dedicate about 25% of her time to the project. She will carry out the majority of the laboratory experiments and contribute to the data analysis and reporting.

Additional effort would be expended by other staff in the ACL to acquire Raman spectra.

**Investigator Background**

Nicholas Condon is the Manager of the Analytical Chemistry Laboratory (ACL) at Argonne National Laboratory (ANL) in the Chemical and Fuel Cycle Technologies Division. He has a PhD in Analytical Chemistry from the University of Wisconsin at Madison. The ACL specializes in solving problems in the analysis of energy and radiological materials, as well as for forensic and security applications. His past work has covered a wide range of topics in optical and analytical science. **Past LDRD Project**: Co-PI on 2020-0291 (Swift 2020), “Millifluidic Optical Cell to Measure Uranium Hexafluoride Hydrolysis Reaction Dynamics,” k$35. The target sponsor (NA-221) was briefed twice on the project, and the new modeling capabilities developed for this project will be a valuable resource for attracting and executing work for a variety of sponsors.

J. Taylor Childers is a computational scientist at the Argonne Leadership Computing Facility (ALCF). He has a PhD in Particle Physics from the University of Minnesota and worked as a fellow at the CERN laboratory in Geneva, Switzerland, where he helped operate and analyze data from the ATLAS experiment. As a scientist in the Data Science Group at ALCF, he has worked with scaling simulation and machine learning codes on supercomputers while continuing to research applications of machine learning to scientific domain problems.

**Project Plan**

**Resources**

The overall budget for the proposal will be k$250 per year for each of FY22 and FY23. This will primarily cover effort. Since the ACL already has a portable mass spectrometer and other analytical instrumentation on hand, no equipment purchases will be necessary. Chemical samples for testing and general laboratory supplies will cost about k$16 per FY. A small Director’s Discretionary (DD) allocation on ThetaGPU might be required for doing the machine learning studies when they are ready to run.

All experimental work will be performed under the ACL General Operations WCD, #60234, which is continuously maintained in an approved and authorized state.

**General equipment, M&S, travel**

**Other**

**Research Milestone**

**Goal Date**

Final Milestone: Demonstrate the use of an AI/ML system to identify the provenance of test chemical samples based on their mass spectra and Raman spectra.

09/30/23

Renewal Milestone: Demonstrate observable differences in mass spectra and/or Raman spectra between test materials from different manufacturers.

06/01/22




**Return on Innovation**

**Outcome**

The expected outcome of this work, if we meet our research goals, is a demonstration that portable instrumentation combined with a trained DNN can provide provenance information about residues related to chemical weapons. This would allow Argonne to occupy a unique niche in the chemical forensics space, one that combines real-world practicality with leading-edge computing techniques. This could be leveraged to market ourselves to existing and emerging sponsors of work in this area.

**Roadmap**

We have currently been working with Jennifer Steeb and the National Security Program to cultivate contacts in several offices, including DHS, DOE-NNSA, and the DoD. We would aim to submit proposals based on this work to one or more of these agencies no later than the FY24 funding cycle.

**References**

[^1]: Z. Witkiewicz, S. Neffe, E. Sliwka, and J. Quagliano, "Analysis of the Precursors, Simulants and Degradation Products of Chemical Warfare Agents," _Critical Reviews in Analytical Chemistry,_ vol. 48, no. 5, pp. 337-371, 2018/09/03 2018.

[^2]: J. J. Moran, C. G. Fraga, and M. K. Nims, "Stable-carbon isotope ratios for sourcing the nerve-agent precursor methylphosphonic dichloride and its products," _Talanta,_ vol. 186, pp. 678-683, 2018/08/15/ 2018.

[^3]: K. H. Holmgren _et al._, "Part 1: Tracing Russian VX to its synthetic routes by multivariate statistics of chemical attribution signatures," _Talanta,_ vol. 186, pp. 586-596, 2018/08/15/ 2018.

[^4]: D. Jansson _et al._, "Part 2: Forensic attribution profiling of Russian VX in food using liquid chromatography-mass spectrometry," _Talanta,_ vol. 186, pp. 597-606, 2018/08/15/ 2018.

[^5]: K. Höjer Holmgren _et al._, "Synthesis route attribution of sulfur mustard by multivariate data analysis of chemical signatures," _Talanta,_ vol. 186, pp. 615-621, 2018/08/15/ 2018.

[^6]: J. Acquarelli, T. van Laarhoven, J. Gerretzen, T. N. Tran, L. M. C. Buydens, and E. Marchiori, "Convolutional neural networks for vibrational spectroscopic data analysis," _Analytica Chimica Acta,_ vol. 954, pp. 22-31, 2017/02/15/ 2017.

[^7]: D. Ma, L. Shang, J. Tang, Y. Bao, J. Fu, and J. Yin, "Classifying breast cancer tissue by Raman spectroscopy with one-dimensional convolutional neural network," _Spectrochimica Acta Part A: Molecular and Biomolecular Spectroscopy,_ vol. 256, p. 119732, 2021/07/15/ 2021.

[^8]: K. Kukula _et al._, "Rapid Detection of Bacteria Using Raman Spectroscopy and Deep Learning," in _2021 IEEE 11th Annual Computing and Communication Workshop and Conference (CCWC)_, 2021, pp. 0796-0799.

[^9]: "Volume 1: Chemical Weapons-Related Common Control Lists," in "Australia Group Common Control List Handbook," 2018.