---
title: 'Final Project'
subheadline: 'Single Neuron BCI'
description: "mouse control activity of single neuron to recieve water reward"
featured_image: '/images/final_proj_banner.jpg'
menu:
  main:
    weight: 3
draft: false
---

Image source: https://3d.nih.gov/entries/3DPX-020130 ramon y cajal drawings

I will talk about my final project here. For now Im copying my app to this class over :) 

My name is Emma Odom and I am a third year PhD student in Brain and Cognitive Sciences here at MIT. I study how neural connectivity gives rise to a physical representation of motor information in the brain and how it evolves over time. That has led me to want to build a BCI where we train mice to control the activity of a single neuron in order to receive a water reward. Imaging neural activity with this BCI offers me precise knowledge of the information contribution of each input to the single neuron and an ability to manipulate each individual component to see how it affects neural circuit dynamics.  Today I heard many with interests in BCI, and what I can offer is access to neural activity in living, behaving mice via a cranial window into their brain!
 
Have done: Built behavioral rig for water reaching task in mice.
Task: Mouse holds bar for 1.5 seconds to trigger solenoid to open and deliver water to spout. Mouse needs to reach for water.
- Simple circuit for capacitance sensing and solenoid control
- Live data acquisition and buffered saving
- Centralized control via Jupyter notebook within VSCode
- Code repo: https://github.com/surlab/Behavior_Code_Emma.git
 
Future: Single neuron BCI
- Real time processing of in-vivo 2-photon imaging data
- Closed loop control of a linear actuator and solenoid valve to deliver water reward
- Alignment of data from capacitance sensors, motorized components, behavioral camera, and 2-photon microscope.
- Safety controls for mouse (it’s alive), microscope (it’s sensitive) + electronics (there’s water involved)

{{< image-figure src="images/bci_fig.jpg" caption=" " size="100%" align="center" >}}

__Figure 1 Single Neuron BCI Task__ _(A) The activity of a single neuron in the primary forelimb motor cortex (MOp) is coupled to the lick spout via a transfer function f. The single neuron’s output activity will be reported in red, and the inputs from other neurons will be reported in green. (B) The presynaptic inputs to the BCI neuron will be imaged as the brain learns and transitions between different BCI transfer functions. The single neuron BCI is crucial to linking synaptic mechanisms to information encoding in neural circuits._

Very relevant inspo [here](https://www.eneuro.org/content/early/2024/09/11/ENEURO.0079-24.2024) and resources (below) for my project.
- [Directional Reaching for Water as a Cortex-Dependent Behavioral Framework for Mice](https://pubmed.ncbi.nlm.nih.gov/29514103/)
- [Skilled reaching tasks for head-fixed mice using a robotic manipulandum](https://www.nature.com/articles/s41596-019-0286-8)