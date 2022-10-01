---
layout: post
title: Using ngSpice with KiCAD for basic circuit simulation
subtitle: Learning and applying circuit topologies using spice
published: true
tags: [NgSpice, Simulation, Circuit Topology, KiCAD]
---


## Simulation - Showcase

![RC circuit](https://github.com/hbchaney/Blogging/blob/master/KiCAD_simulations/RC_Circuit/imgs/Basic_RC.png?raw=true)

### My Background

Initially when I learned circuits back in my sophomore year of undergrad I was not that interested. I found it very abstract and did not see the point. From the projects I have been doing, I have realised that I need to catch up. Having something to apply circuit knowledge to has made learning circuits much more interesting.  

I had bought a starter pack of basic components and made some simple circuits. I found that using a multimeter and probing the live circuit taught me so much more than just calculating it on paper. 

### Why Simulation? 

Not all circuits are cheap and easy to breadboard. With simulation you don't have to worry about having all the specific parts on hand to see how the circuit will work. Some Circuits also require an oscilloscope to properly analyze. I would love to use one, but they are a bit too expensive at the moment. 

When learning to make circuits, mistakes are inevitable. Rather than destroy components in the real world, simulations give a much more forgiving learning experience. Real world circuits can also get dangerous at higher voltage and current levels.

### Simulation Example

Full Bridge : 

![full bridge](https://github.com/hbchaney/Blogging/blob/master/KiCAD_simulations/Full_Bridge/images/full_bridge.png?raw=true)

One of the issues with spice is that voltage is relative to the zero point rather than testing the voltage difference in two locations. This makes the output voltage not appear to be in the correct orentation. 

--- 

### Starting Simulations: 

I followed [this](https://ngspice.sourceforge.io/ngspice-eeschema.html) guide to make the simulations and get started. 

I started with a basic RC circuit of both AC and PWM voltage sources and worked up from there.

