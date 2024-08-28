---
layout: work
title: "Molecular Fingerprints"
description : Coarse-Grained Configurational Polymer Fingerprints for Property
Prediction using Machine Learning"
caption: Coarse-Grained Configurational Polymer Fingerprints for Property
Prediction using Machine Learning
tags: ["Deep Learning", "PyTorch", "Monte Carlo simulation","C++"]

thumbnail-img:
share-img:
comments: true
gh-repo: Ishan-Kumar2/configurational-polymer-fingerprint
gh-badge: [follow]
dated: May 2021 - April 2022
---


<img src="https://github.com/Ishan-Kumar2/configurational-polymer-fingerprint/blob/main/polymerfingerprint.png" width="600">

- Present a novel method to generate a ***configurational level fingerprint*** for polymers using the Bead-Spring-Model.
  - Previous fingerprinting approaches that employ monomer-level information where atomistic descriptors are computed using quantum chemistry calculations, this approach incorporates configurational information from a coarse-grained model of a long polymer chain.
- This proposed approach is advantageous for the study of behavior resulting from large molecular weights.
- We make use of two kinds of descriptors.
  - Geometric descriptors like $Re^2$, $Rg^2$ etc - Calculated Descriptors.
  - Generate a set of data-driven descriptors using an unsupervised autoencoder model - Learnt Descriptors.
  - Using a combination of both of them, we are able to learn mappings from the structure to various properties of the polymer chain by training ML models.
- We test our fingerprint to predict the probability of occurrence of a configuration at equilibrium, which is approximated by a simple linear relationship between the instantaneous internal energy and equilibrium average internal energy.

This work was done as part my final year thesis project with the Drug Discovery and Molecular Simulation Lab, IIT Roorkee under the wonderful guidance of Prof Prateek K Jha. This work received the ***Aastha Dixit Mukul prize*** for being the best thesis in the batch of 2022 at the Convocation ceremony by a panel of Industrial and Research experts.

arXiv link - https://arxiv.org/abs/2311.14744


<center>
<a class="btn-github" href="https://github.com/Ishan-Kumar2/configurational-polymer-fingerprint" >
  View on Github
</a>
</center>
