---
title: 02 Zoning Problem - Agent Behaviours
date: "2021-06-01"
tags:
  - Agent based Modelling
  - Artificial Intelligence
  - Zoning problem

keywords:
  - architecture
  - Artificial Intelligence
  - Agent based Modelling

cover: ../Images/zoning/Agent_Behaviours.gif
description: The article explains the logic behind the Agent behaviours in the multi-agent system designed for the zoning problem.
showFullContent: false
---

# Agent Behaviours

The third part of the multi agent system are the agents. Before starting with description of the various agent behaviours developed in the project certain terminology used in the text is described as follows:

`1.Agent:`An agent is anything that can be considered able to perceive its environment through sensors and act on this environment through actuators.

`2.Multi-Agent system:`An agent-based system also can exist with several agents having the characteristics as described in the previous paragraph. Such a system is called as a multi-agent system.

`3.Agent Behaviors:` The actions which the agent can perform to achieve its goals.

`4.Stencil:` The neighborhood definition in a discrete 3d space.

In the project several agent behaviours were developed. They can be classified into three main criterias _Agent Origin, Occupy/Unoccupy and Attraction/Repulsion._

# Stencils

In order to create a boundary for scanning the neighbourhood around a voxel several stencils were defined.The function stencil is available in the library Topogenesis where by default there can be two types of neighbourhoods. The first one is the von neumann neighbourhood containing 6 neighbouring voxels and the second is the moore neighbourhood containing 26 neighbouring voxels.The library also contains function to make the center as unoccupied for the stencil.

The other stencils developed are derived from these two main stencils. The four neighbourhood and the eight neighbourhood stencil are especially programmed for two dimensional agent behaviours where the available neighbours on only a particular axis are considered.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Stencils.png" >}}

**Stencils developed for the agent behaviours**

The full floor lattice and the full lattice are considered for searching the whole search space in two dimensions or three dimensions.The full floor lattice considers the maximum extents of the horizontal or vertical slice and the full lattice considers the complete 3d lattice.

# Occupy/Unoccupy Behaviour

The `Occupy behaviour` is a class of behaviours which the agent can perform to occupy certain voxels based on their values and neighbourhood condition in a voxelated lattice. The occupy behaviour can be further classified into two dimensional and three dimensional behaviours depending on the stencil which determines their neighbour search space.

The occupy behaviour works in the following manner. The first step involves identifying the neighbours based on a selected stencil from the stencils described in the previous section.The desirability value for each voxel can be derived form the performance lattice as described in [Performance criteria](/posts/zoning-problem-mcda) which becomes the environment lattice for the agent to perform the behaviour. The values in the environment lattice for the identified neighbours in the occupancy lattice are extracted and the best or the worst value is picked by the agent and the corresponding voxel is occupied.This process goes on till the number of voxels occupied by the agent is satisfied.
The generalised pseudocode for the same is shown below:

```python
# Load base lattice and Desirability lattice from previous steps
Base_lattice=[ixjxk]
Desirability_lattice=[ixjxk]

# Define the behaviour requirements
Number= [int] # number of voxels agent needs to occupy
# Define the stencils required
stencil = tg.createstencil(”vonneumann”,1, 1)

# Define the Agent class
agent():
def __init__(self,origin,stencil,id):
origin = voxel id or origin voxel
stencil = neighbourhood definition
id = unique number to trace agent behaviour

# def Agent_behaviour(self,env):
neighs = origin.findneighbours(stencil) # retrieves neighbours based on stencil
# Filter out available neighbours
avail_neighs = Base_lattice[neighs==1]
# In case of no neighbours available
len(avail_neighs) == 0
then:
stencil == bigger stencil
# Find corresponding value from desirability lattice for available neighbours
vals = valuelattice [availneighs]
# select the highest valued neighbour
selectedvoxel=baselattice[np.argmax(vals)]

# Modify the origin
new_origin = selected_voxel

# Loop until the number of voxels that need to be occupied is met

```

All the behaviours can be tried using this binder link: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/adityasoman/GEN-ARCH_Binder/61837cfde296ad9ee000b937d9f3c8db62dbd6d8?filepath=02.Zoning_problem%2FAgent_behaviours%2FAgent_behaviours.ipynb)

## 2D Rectangular growth behaviour

In this behaviour the primary stencil used to find the neighbours is the`4 neighbourhood one.` After the values of the neighbours are retrieved from the environment lattice the maximum valued neighbour is picked for the next iteration. The values for neighbours of neighbours get a boost in this type of behaviour hence the occupancy pattern for the agent is in a rectangular manner. If the behaviour reaches a point where no neighbours are available for occupancy then the search space is gradually increased to 8 neighbourhood area and finally to the full floor lattice.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Rectangular.gif" >}}

**2D Rectangular growth behaviour**

## 2D Circular growth behaviour

In this behaviour the primary stencil used to find the neighbours is the `8 neighbourhood one.` The rest of the nature of the code is similar to the rectangular one. The main reason for this circular growth is due to the combination of selection of the 8 neighbourhood search space from the first instance and the boosting of values for the voxels whose neighbours have been occupied.This type of growth patterns where the neighbours of neighbours are given a preference ensures the topological nature of the spaces where characteristics like having a single island and no holes in the structure are maintained.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Circular.gif" >}}

**2D Circular growth behaviour**

## 2D Random growth behaviour

In this behaviour the primary stencil used to find the neighbours can be `4 or 8 neighbourhood one.` The maximum valued neighbour is picked and no boost is given in the values for neighbours of neighbours. This leads the agent to purely follow the values of the environment lattice as the basis for occupancy. This behavior has its advantages when it comes to achieving the maximum valued voxels for a function due to its singular nature in selection but it can also lead to a haphazard growth with many islands in its graph structure and with holes in between.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Argmax_2d.gif" >}}

**2D random growth behaviour**

## 3D Spherical growth behaviour

In this behaviour the primary stencil used to find the neighbours is the `26 neighbourhood one.` This allows for selection in three dimensions. The neighbours for each agent position are stored in a list which is referred in every iteration to check for neighbours of neighbours. In this behaviour a boost is given based on the number of adjacent neighbours to a voxel under consideration. This boost creates a behaviour which forms a spherical pattern around the agent origin picking the best possible values in the environment field with the added boost based on neighbourhood occupancy condition.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Spherical.gif" >}}

**3D Spherical growth behaviour**

## 3D Cuboidal growth behaviour

In this behaviour the primary stencil used to find the neighbours is the `6 neighbourhood one.` Similar to the Spherical behaviour the neighbours for each agent position are stored in a list which is referred in every iteration to check for neighbours of neighbours also a boost is given based on the number of adjacent neighbours to a voxel under consideration.

The chances of this behaviour running into conditions where there are zero neighbours is higher since it only considers vertically and horizontally connected neighbours and not the diagonal ones, hence the secondary stencil in this case is the Moore neighbourhood one and finally the tertiary one being the full lattice one so that the agent has the chance to move away from the no neighbour position and restart at a different location.This boost along with the stencils creates a behaviour which forms a cuboidal pattern around the agent origin picking the best possible values in the environment field with the added boost based on neighbourhood occupancy condition.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Cuboid.gif" >}}

**3D Cuboidal growth behaviour**

## 3D Random growth behaviour

The 3d random growth behavior is similar to the 2d random growth behavior one but with a different stencil sets. In this behaviour the primary stencil can be the 6 neighbour Von-neumann stencil or the `26 neighbour Moore neighbourhood` thus enabling a three dimensional behaviour. The selection of voxels is based on the argmax of the values form the available neighbours and there is no preference for neighbours of neighbours.This leads to a better output in terms of capturing the higher performing voxels for the agent but the topological requirements of single island and no hole polynomio are not satisfied. Ideally these behaviours can be used to unoccupy poorly formed shapes in the zoning model or occupying non connected discrete spaces.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Argmax.gif" >}}

**3D random growth behaviour**

## Attraction/Repulsion Behaviour

The 3d growth behaviour of agents towards each other or away from each other can be classified as attraction/repulsion behaviour.The behaviour can be used for either growing (occupying) voxels towards each other or just for finding locations in the graph (generated out of voxelated grid) satisfying certain closeness requirements.

The steps for generating the agent behaviours are as follows:

First from a voxelated grid using the Von-neumann stencil as a connectivity relation a graph is created.The generation of the graph is done using the library [network x](https://networkx.org/). The minimum distance from all the voxels to the rest of the voxels are generated using the Flyod Warshall algorithm for finding the minimum distances.

Then the points of interest or voxels of interest are choosen from the grid and the distance matrix for them are generated using the output from the Floyd Warshall algortihm. Distance matrix is nothing but the graphical distance or Manhattan distance from each voxel to the voxel of interest.

Once the distance matrices are generated for both the points of interest they are used as environment lattices for the agent based simulation for the agents to grow or move towards each other depending on the use case

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/zoning/Attraction.gif" >}}

**Attraction/Repulsion Behaviour**
