---
layout: post
title:  "Paper Development Process: Part Two, Machining Success"
date:   2020-10-09 17:11:09 +0000
tags: [PaperDevelopment, PhD, ProblemSolving]
---

In a stroke of good fortune, one major development has occurred since the last instalment of this series, the return to laboratory work!
As such I have ben able to get hands on with the equipment that will be utilised in this study and quickly iterate the apparatus design.
With that, let's briefly review the methods currently used for virtualising grains that inform the path towards our chosen apparatus type.

## Grain Virtualisation Techniques

To virtualise *any* real world object, there first needs to exist some input on which an algorithm carries out mathematical operations to leave a three dimensional array of points, representing the surface of a particle. 
This input by its nature optical, though in varying ranges of the electromagnetic scale. 
During the first draft of my literature review, I focused on two methods that, to my mind, offer the most accurate virtualisation of three dimensional grains, 3D X-Ray Computed Tomography (3DXRCT) and image based grain reconstruction. 

The former was used in Medina/Jereves' study *A geometry-based algorithm for cloning real grains 2.0* [[1]](#1). 
In this study, a complete 11mm diameter triaxial cell was scanned using 3DXRCT. 
The raw output of which is numerous 2D slices of the sample, which were reconstructed into 3D representations of each particle using a [level-set framework](https://en.wikipedia.org/wiki/Level-set_method). 
This method leverages the main benefit of 3DXRCT in the context of grain virtualisation, the ability to scan large numbers of particles at a time regardless of orientation.

The latter method, image based grain reconstruction, was utilised in Nadimi/Fonseca's study *Single-Grain Virtualization for Contact Behaviour Analysis on Sand* [[2]](#2).
This method, neatly summarised in the below figure from their study, uses multiple projections of the particle generated by images around the particles central axis to reconstruct the surface of the particle.

![Schematic of projection method used by Nadimi and Fonseca](\DevProcessPart2\NadimiFonsecaSchematicProjection.png)
*Schematic of projection method used by Nadimi and Fonseca [[2]](#2)*


As shown in the figure, a binary of the particle outline from each image around the particle is extruded by some arbitrary depth.
The intersection of all of these extrusions represents the surface of the particle, with more extrusions comes a greater resolution representation of the object in question. 
Indeed in the study in question, a 5 µm per voxel resolution was achieved from 30 images.

Both methods have their merits, and fortunately the University of Nottingham Department of Materials, Manufacturing and Mechanical Engineering has an X-Ray tomographic scanner that can be used. 
However, as mentioned in the last instalment, grain virtualisation in this instance is to be used in conjunction with single particle shearing. 
It is imperative for the latter stages of this study that the orientation of the grain as it is sheared against the interface surface is known.  
As such, 3DXRCT is **not** a viable option as it would force the inclusion of two further steps in the experimental process: detection of the specific particle being tested (there are hundreds of particles in each sample), and calculation of the orientation of the particle in relation to the interface surface.
Hence image based grain reconstruction will be utilised by designing a method to work symbiotically with the single particle shear apparatus.


## Imaging the Particle

A schematic of the apparatus used to image grains is provided by Nadimi/Fonseca [[2]](#2).
Shown below, this system consists of a particle mounted to the end of a stepper motor, controlled by a interface that also captures images at certain angles of rotation around the particle. 

![Schematic of the imaging apparatus used by Nadimi and Fonseca](\DevProcessPart2\NadimiFonsecaSchematicApparatus.png)
*Schematic of the imaging apparatus used by Nadimi and Fonseca [[2]](#2)*

### Apparatus Components

A similar apparatus can be easily implemented in the Nottingham Centre for Geomechanics laboratory, using existing equipment. 
A stepper motor and encoder currently sit idle as improvements to the direct interface shear apparatus have made these components obsolete. 
The stepper motor communicates over an RS232 -> USB adapter, allowing for a range of devices to control its function. 
High resolution [Teledyne DALSA Genie Nano](https://www.teledynedalsa.com/en/products/imaging/cameras/genie-nano-1gige/) cameras are used within the lab for computer vision applications to monitor sample movements in the centrifuge as well as in direct interface shear.
A C-mount allows for standard microscope lenses to be attached to the camera, giving very detailed images, which are required to capture the sand grains which have a mean diameter of 1.18mm.
These Gigabit Ethernet cameras operate over the GeniCam standard allowing them to be controlled by a range of software, but more on that next time...

### Prototyping an apparatus

Using the Nadimi and Fonseca [[2]](#2) apparatus as inspiration, prototyping the apparatus which pairs up the stepper motor and camera can be achieved using their CAD files within a design package such as Autodesk Inventor. 
An important requirement of any design is for adjustment in the relative position of the camera sensor in reference to the motor shaft, to optimise the focus of the image depending on the lens and size of particle being imaged.
Also, each particle scanned would be subsequently tested in a single particle shear experiment.
As such, the particles would be glued to an M5 hex bolt so they can easily be mounted on the end of a 20N load cell.

Prior to any parts being drawn in inventor, I drew a quick sketch of the geometry required to give me something to work towards, as shown below.

![Initial sketch of apparatus](\DevProcessPart2\ParticleScanningSketch.png)
*Initial sketch of apparatus*

As shown, I decided the best way to control the focus and centre point of the lens (to account for optical distortion) was to use a series of slots.
I couldn't think of a reason why this wouldn't be sufficient at the time (though on second viewing its far too complex), so I moved on to the prototyping phase in Autodesk Inventor 
As mentioned in the previous instalment, I planned to use 3D printing for this particular task, so I set about designing the pieces of the apparatus in accordance to the printing limits of our 3D printer.
As a consequence of this, and due to my inexperience with the technology, each of the pieces is rather bulky and would be subject to long manufacture times. 

Shown below is the final prototype I designed to fit the geometry of the stepper motor, gearbox and GigE camera.

![Prototype of apparatus including motor, gearbox and camera .stl files](\DevProcessPart2\ParticleScanningInventorProject.png)
*Prototype of apparatus including motor, gearbox and camera .stl files* 

Overall, its a package that certainly achieves its objectives, and isn't all that different from the one used by Nadimi and Fonseca [[2]](#2), though will certainly take a good amount of time to produce and assemble. 
Now all that remains seen as I have access to the lab again is to manufacture the parts and begin to experiment with controlling the motor and camera in tandem. 

### Best laid plans
<p class="message">
The idea was there, the execution, just not quite right... - Martin Tyler
</p>

Before covering what the final implementation of the camera mount assembly turned out like, its worth covering why actually I wanted to use 3D printing to begin with.

- I had assumed that the lab technicians responsible for fabrication would not be available to machine any parts when I returned to the lab
- 3D printing is an excellent way to enable others to manufacture similar parts from my designs, helping this study become more of an open-source endeavour
- It gives me the opportunity to add another skill to my arsenal 

Fundamentally, there is no reason why a fabricated metal part could not replace my 3D printed parts, provided the technicians were available to manufacture them.
Fortunately, Steve the technician was available and happy to help.

On returning to the lab I had the chance to physically refamiliarise myself with the motor and gearbox assembly.
The assembly had previously been used as a normal load actuator for our macroscopic direct shear apparatus - before I made it obsolete by replacing it with pneumatic actuator for better stiffness control [[3]](#3) - which was attached to a bracket that sat proud of a keywayed bushing connected to the gearbox drive shaft.
This provided an opportunity.
A simple M5 threaded insert to the bushing allowed for the M5 bolt the particles are glued to, to be attached to the motor assembly.
The thread has the benefit of allowing adjustment of its position relative to the perpendicularly mounted camera. 
You can see the previously mentioned bracket and bushing with the M5 insert in the image below

![Bracket, bushing and M5 insert of the motor and gearbox assembly](\DevProcessPart2\BracketBushingM5.jpg)
*Bracket, bushing and M5 insert of the motor and gearbox assembly* 

So, if I could design a metal plate that allows for control of the focus position of the lens, the design constraints from earlier would be satisfied in a much simpler package than the prototype design. 
This was achieved using some CAD, [cardboard aided design](https://youtu.be/9VKegYsSRG0?t=113). 
After drawing out a scaled template of what will be 3mm mild steel plate, complete with slotted 3mm holes for fixing the position of the Genie Nano camera, Steve was able to whip up the part in no time.
You can see the final completed assembly in the image below

![Completed particle imaging assembly](\DevProcessPart2\CompletedAssembly.jpg)
*[Completed particle imaging assembly* 

Overall this is a much simpler package than originally prototyped.
The vertical position of the camera can easily be set using the M3 bolts through the slotted plate, and the centrepoint of the particle is neatly adjusted by the M5 thread.
The cut-out hole allows for a greater amount of light to surround the particle, useful when using long exposure times 

One could say that the time and effort spent prototyping the 3D printed components was wasted time, and with the benefit of hindsight one would be absolutely right.
However, it wasn't a horrible idea, just not the optimal solution when circumstances changed, so no harm done. 

## Objectives

Reviewing the progress to this point, we can mark a tick in our list!
We have an apparatus that works and has fine control of the focus point and centre point of the lens. 
The lessons learnt here are probably:
1. Keep it simple, stupid 
2. Novel technologies and use cases are cool and all, but if they can't improve on the tried and tested, there's no good in forcing their use

- [x] Develop an apparatus allowing for computer imaging different angles of a particle
- [ ] Develop a reliable motor and camera control application
- [ ] Develop a framework to stitch together a 3D virtual particle from 2D images of different angles
- [ ] Extend the capabilities of 2D shape analyses to work on our 3D virtual particle
- [ ] Use the 3D virtual grain in a virtual particle shear experiment

The eagle-eyed among you may note the addition of an extra checkbox, 'Develop a reliable motor and camera control application'.
Luckily, you won't have to wait too long to find out more about this, as that's the next job to tackle.

See you in the next one. 

## References

<a id="1">[1]</a> 
Medina, D. A. and Jerves, A. X. (2018). 
A geometry-based algorithm for cloning real grains 2.0
Granular Matter, 21, 2.
DOI: 10.1007/s10035-018-0851-9

<a id="2">[2]</a> 
Nadima, S. and Fonseca, J. (2017). 
Single-Grain Virtualization for Contact Behavior Analysis on Sand
Journal of Geotechnical and Geoenvironmental Engineering, 143(9), 2.
DOI: 10.1061/(ASCE)GT.1943-5606.0001740

<a id="3">[3]</a> 
Pettey, A. and Heron, C. (2020)
Effect of Crushed Particles on Soil-Structure Interface Behaviour
4th European Conference on Physical Modelling in Geotechnics, Luleå, Sweden
URL: <https://www.researchgate.net/publication/344612088_Effect_of_Crushed_Particles_on_Soil-Structure_Interface_Behaviour>