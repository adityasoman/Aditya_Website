---
title: Massing Problem
date: "2021-05-31"
tags:
  - Multi-criteria Decision analysis
  - Human-Machine Co-design
  - Participatory design 
cover: ../Images/Massing_problem_Cover.png
keywords:
  - architectural design
  - computational design 
  - participatory design
  - open buildings
description: Massing problem solution which involves finding the appropriate volumetric design of the building as the base for futher configurational resolution.
showFullContent: false
---
# Massing Problem

The problem of finding the appropriate volumetric design of the building is the highest level of the space layout problem. In this stage the impact of placing volumes representing the built mass on the site is studied with respect to its effect on the surrounding buildings as well as its own performance in achieving the urban level design goals.

# Aim

To generate various massing variants for the site and select a variant which will maximise the site utilization without compromising on the quality of the spaces as defined by the architect.

# Process

The massing process described further is particular to the case at hand at Buiksloterham and Co.The process taken in this step is a combination of manual design and  computational analysis and validation. The design ideas are sketched manually and the performance indicators for the sketches are programmed in a computational framework where simulations and calculations are done to quantify the indicators. Then weights are given to each criteria based on the designers validation preferences and a `Multi-criteria decision analysis` is done to rank and select the design variant from the sketches.This process also takes place in a methodical and ordered way in several steps as described below:

Looking at the space program two distinctions can be made regarding the massing requirements of the program.The mass encompassing the volume of Self development plots and the mass encompassing rest of the space program.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Space_program.jpg" >}}

`The first step` of the process involves creating all the logical variants of the basic distribution of the two masses along with the connecting road network and running the simulations for Sunlight hours and Visibility on them.The basic intention of running these simulations is to pick an option having maximum visibility and sunlight hours on the building forms and the minimum shading of the self development plots by the buildings.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Site_Diagram_Simulations.jpg" >}}

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Stage01.jpg" >}}

The variants where self development plots were placed in the center of the site were eliminated due to the possibility of shading due to the taller buildings surrounding them. In the visibility simulation points of interest on the IJ river Front access road and the canal where a pedestrian bridge is proposed is considered with equal weightage for visibility from all points of interest.The modelling and simulation process is done on Rhino and Grasshopper with the plugin Ladybug for environmental simulations.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Massing_problem/Massing_Problem.jpg" >}}

`The Second step` of the process involves designing of built and unbuilt spaces (Green spaces,Open public spaces) inside the massing reserved for accommodating the space program.A maximum height of 60m was considered looking at the new developments in the site surroundings.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Stage02.jpg" >}}

Various design variants were developed and certain set of simulations were selected for defining the performance of the variant which was followed by comparison and eventual selection of the variant.  _The simulations used for this stage include the Total Daylight hours simulation,Visibility simulation, Access to Sky from the Unbuilt spaces, Total built space/Sunlight hours,Total floor area (considering an arbitrary floor height of 3m), Total Unbuilt Space, Total built space / Total unbuilt space_. The simulation values are recorded in an excel file and then the MCDA process is performed to rank and select the best options from the generated variants. The reason for certain calculations like the ratio of the built/green spaces or the ratio of the floor area with the sunlight hours was considered to _avoid designing bigger volumes for a better performance_.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Massing_problem/Massing_Problem2.jpg" >}}

In the `The Third step` involves refinement of the massing developed in stage two. The design is analysed in terms of its suitability for development of floor plans for the space program  based on the derived dimensions and the best combination of the base shape and height of the blocks are explored by converting the top ranked massing options from stage two into parametric models.The parametric models are then linked to the simulation runs from stage two and an evolutionary solver is used to find the right combination of the parameters. The objective function for the solver is to maximise the weighted product of the defined simulation parameters. Constraints are given to the base and height of the blocks according to the design  problem formulation.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Massing_problem/Massing_Problem4.jpg" >}}


# Limitations

The massing process described in the previous sections is very subjective in terms of its appropriateness towards designing a building mass.The idea behind the process was to experiment with a methodical way of breaking down the design process into smaller steps so that the decision making process in the whole problem is traceable and does not directly jump into conclusions. With an increase in the accessibility of computational tools and parametric modelling software this whole generation process can be different as long as final outcome of the process (finding the location of built mass on site)  can still be used for the next problem in spatial configuration.


# Conclusions

The MCDA methods used in operations research could potentially be a way of making decisions in a design process if the problem is clearly defined as seen in the massing problem.The machine human collaboration process in the massing problem uses the calculation power of machines and the design intelligence of humans to  generate a final massing model will represent the boundary for the zoning problem and the massing will be further discretised into smaller voxels  which will further be used to generate various lattices for the multi agent system approach taken in the zoning problem. The whole problem of massing could also be viewed in a different manner where the machine can be trained to generate the massing option by determining if a certain voxel or volume should exist on the site or not, that said it has a huge scope and can be a thesis project on its own. Finally to conclude this stage of design the the massing model will be saved as an .obj file and the voxelization process will be done on Python using the meshing python library [Trimesh](https://trimsh.org/trimesh.html) and the python library [Topogenesis](https://topogenesis.readthedocs.io/notebooks/random_walker/)

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Massing_problem/massing_to_zoning_problem.png" >}}
