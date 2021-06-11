---
title: 02 Zoning Problem - Agent Behaviours
date: "2021-06-03"
tags:
  - Enviornmental simulations
  - Zoning problem 

keywords:
  - architecture
  - Ladybug Tools
  - Enviornmetal simulations

cover: ../Images/Quiteness_lattice.png
description: The article explains the simplified enviornmetal simulations done for generating a base for decision making. 
showFullContent: false
---
# Agent Behaviours

The third part of the multi agent system are the agents. Before starting with description of the various agent behaviours developed in the project certain terminology used in the text is described as follows:

1.Agent:An agent is anything that can be considered able to perceive its environment through sensors and act on this environment through actuators.

2.Multi-Agent system:An agent-based system also can exist with several agents having the characteristics as described in the previous paragraph. Such a system is called as a multi-agent system.

3.Agent Behaviors: The  actions  which  the  agent can perform to achieve its goals.

4.Stencil: The neighborhood definition in a discrete 3d space.


In the project several agent behaviours were developed. They can be classified into three main criterias _Agent Origin, Occupy/Unoccupy and Attraction/Repulsion._


# Stencils

In order to create a boundary for scanning the neighbourhood around a voxel several stencils were defined.The function stencil is available in the library Topogenesis where by default there can be two types of neighbourhoods. The first one is the von neumann neighbourhood containing 6 neighbouring voxels and the second is the moore neighbourhood containing 26 neighbouring voxels.The library also contains function to make the center as unoccupied for the stencil.


{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Privately%20Owned%20Housing.png" >}}

**Moore Neighbourhood stencil (26 neighbourhood)**


{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Privately%20Owned%20Housing.png" >}}

**Von Neumann Neighbourhood Stencil (6neighbourhood)**

The other stencils developed are derived from these two main stencils. The four neighbourhood and the eight neighbourhood stencil are especially programmed for two dimensional agent behaviours where the available neighbours on only a particular axis are considered.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Privately%20Owned%20Housing.png" >}}

**Moore Neighbourhood stencil (26 neighbourhood)**

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Argmax.gif" >}}

**Von Neumann Neighbourhood Stencil (6neighbourhood)**

The full floor lattice and the full lattice are considered for searching the whole search space in two dimensions or three dimensions.The full floor lattice considers the maximum extents of the horizontal or vertical slice and the full lattice considers the complete 3d lattice.


# Occupy/Unoccupy Behaviour

The Occupy behaviour is a class of behaviours which the agent can perform to occupy certain voxels based on their values and neighbourhood condition in a voxelated lattice. The occupy behaviour can be further classified into two dimensional and three dimensional behaviours depending on the stencil which determines their neighbour search space.

The occupy behaviour works in the following manner. The first step involves identifying the neighbours based on a selected stencil from the stencils described in the previous section.The desirability value for each voxel can be derived form the performance lattice as described in [Performance criteria](/posts/zoning-problem-MCDA) which becomes the environment lattice for the agent to perform the behaviour. The values in the environment lattice for the identified neighbours in the occupancy lattice are extracted and the best or the worst value is picked by the agent and the corresponding voxel is occupied.This process goes on till the number of voxels occupied by the agent is satisfied.
The generalised pseudocode for the same is shown below:
