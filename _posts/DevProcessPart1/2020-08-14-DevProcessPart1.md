---
layout: post
title:  "Paper Development Process: Part One, A Computer Full of Sand?"
date:   2020-08-14 14:04:20 +0000
tags: [PaperDevelopment, PhD, ProblemSolving]
---

After nearly five months of squeezing every last ounce of utility out of the experimental data I have access to, the basin has run dry. Unfortunately my seminal journal publication is going to have to wait. However! This drought has forced me to into developing other work to develop into future publications, and I think I have just the idea...

In this series of blog posts I will be detailing the process of developing what _I hope_ will eventually become, or be an integral part of, a future journal paper.
The aim is to provide a neat account of how I go about tackling what can be quite an imposing challenge, and along the way use this format to diagnose any ways in which this process can be made more efficient. 
Also, this series should have the added benefits of holding me to account, as crowds frothing at the mouth cry out for the next instalment; acting as a diary so reviewers to point out the *exact point in time* I made a colossal mistake, marvellous!

Let's begin by defining the motivation and goals of the project and draw up a checklist of problems that need solving.

## Quantifying the Shape of Granular Media

### The motivation

Granular media of any type, be that pills, rice, packaging pellets or sand, come in many different shapes and sizes.
This shape and size has a well documented impact on physical behaviour as grains are exposed to external forces [[1]](#1)[[2]](#2)[[3]](#3).
The specific case of interest for me is how the shape of a grain of sand influences the amount of damage it does to a surface over many cycles. 
In the Nottingham Centre for Geomechanics we have a simple apparatus used to simulate this that I designed last year, a schematic of it is pictured below.


![Schematic of the single particle shear apparatus](\DevProcessPart1\SingleParticleSchematic.png)


The sand particle is held in position under a small load whilst the structural interface (metal plate) is sheared (moved) underneath the particle thousands of times. In many ways its not dissimilar to a stylus moving through the grooves of a vinyl record. 
I can hear you now say "those records don't show an awful lot of damage after **tens** of thousands of rotations, what gives?" Well that is the burning question, what does cause the damage, if any?

Whilst we have empirical knowledge that the shape of grains changes the amount of wear on a surface, and there is plenty of research into the role of shape in granular bodies of thousands of particles, there is surprisingly almost no research that has been conducted into quantifying the influence of shape in *abrasive wear.*
The two categories do appear to have many similarities, though from my research, all prior analyses of shape share a very similar flaw, they have all been conducted in two dimensions, as I have represented the particle in the schematic above. 
Clearly, this fails to represent reality, especially if the particle becomes embedded in the surface. 

Finally, we arrive at the motivation for this project.
We need a robust and repeatable method for taking a grain of sand, and *quantifying the shape in three dimensions.*
To do this, the particle needs to be "virtualised" through computer imagery for analysis.
This has the added benefit of enabling virtual modelling of the experiment mentioned before using an identical shape as in reality.

To speed up development existing tools and hardware will be utilised where possible in addition to 3D printing parts of the apparatus, avoiding the need for fabrication. 

## Objectives

To summarise, the major deliverables for this project are:

- [ ] Develop an apparatus allowing for computer imaging different angles of a particle
- [ ] Develop a framework to stitch together a 3D virtual particle from 2D images of different angles
- [ ] Extend the capabilities of 2D shape analyses to work on our 3D virtual particle
- [ ] Use the 3D virtual grain in a virtual particle shear experiment

With that, the project begins. The next post will answer the question, how do you get a grain of sand into a computer?

## References

<a id="1">[1]</a> 
Kawamoto, R. et al. (2018). 
All you need is shape: Predicting shear banding in sand with LS-DEM 
Journal of the Mechanics and Physics of Solids, 111, 375-392.
DOI: 10.1016/j.jmps.2017.10.003

<a id="2">[2]</a> 
Cavarretta et al. (2016). 
The relevance of roundness to the crushing strength of granular materials
Géotechnique, 67(4), 301-312.
DOI: 10.1680/jgeot.15.P.226

<a id="2">[3]</a> 
Cavarretta et al. (2010). 
The influence of particle characteristics on the behaviour of coarse grained soils
Géotechnique, 60(6), 413-423.
DOI: 10.1680/geot.2010.60.6.413