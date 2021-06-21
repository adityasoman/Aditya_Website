---
title: 03 Unit Assignment Problem
date: "2021-06-02"
tags:
  - 3D Layout problem
  - Unit assignment problem
  - Agent based modelling
keywords:
  - architecture
  - computation
cover: ../Images/Unit_assignment_cover.gif
description: Massing problem solution which involves finding the appropriate volumetric design of the building as the base for futher configurational resolution.
showFullContent: false
---
# Unit Assignment Problem 

 The Unit assignment problem deals with assigning units inside the zones created in the previous layer of the configuration problem. Unit can be defined as a entity in the space program which comprises of a self contained set of rooms collectively catering to a common function. A three room apartment in a zone dedicated for an apartment complex is example of unit inside a zone.

# Aim
The Unit Assignment problem can be classified into two categories:
`The first category` is the zoning problem where there is no closeness relationship between the units of the zone and assigning the units anywhere inside the zone will have equal impact on the assignment goals. An example of this are the units or apartments which are to be assigned inside the zones like the Privately owned housing / Social sector rental housing / Free-Sector Rental Housing. The zones which have been designed for them already satisfy the desirability of the location in the building in the zoning problem itself so the aim at this stage would be to reach the target number of units inside the zone which can be achieved by simple mathematical subdivision of the grid. 

`The second category` of unit assignment problem is similar to the zoning problem where there is a relationship for the closeness of he units to each other and each unit itself has a preference for placement in the zone. The problem in this case would be a higher resolution zoning problem itself with closeness requirements. The aim here would be similar to the zoning problem to achieve the maximum benefit of assignment based on the desirability matrices for the various units considering the constraints of closeness in the problem. The Office zone in the Case of Buiksloterham can be considered as one such problem. 

The units that need to be assigned for the problem case are as follows:

| Zone | Unit | Number of Unit | Number of Voxels per unit |
| - | :-: | :-: | :-: |
| Privately owned housing | Large House | 60% of Zone Volume | 18 |
| Privately owned housing | Medium House | 40% of Zone Volume | 09 |
| Social rental housing | Medium House | 75% of Zone Volume | 09 |
| Social rental housing | Small House | 25% of Zone Volume | 04 |
| Free sector rental housing | Large House | 60% of Zone Volume | 12 |
| Free sector rental housing | Medium House | 40% of Zone Volume | 09 |
| Restaurants and cafe | Restaurant | 70% of Zone Volume | 18 |
| Restaurants and cafe | Cafe | 70% of Zone Volume | 12 |
| Retail Stores ||  100% of Zone Volume  | 4 |
| Offices| Open office spaces | 65% of Zone Volume | NA |
| Offices| Meeting rooms | 15% of Zone Volume | 2 |
| Offices| Cafeteria and common spaces | 20% of Zone Volume | NA |
| Parking| Car Parking | 40% of Zone Volume | NA |
| Parking| Bike Parking | 60% of Zone Volume | NA |

## Steps involved in the Unit Assignment problem:
`Step1:` Interpolation of the Zoning problem output:
The first step in the Unit assignment problem is to make the resolution of the voxelated grid finer from a 6x6x6m size to a 3x3x3m size. This finer resolution will make assigning the units more accurate due to the smaller division size of the area into voxels.

`Step2:`Assigning Vertical and Horizontal Shafts:
In the base lattice consisting of zones and a high resolution lattice with smaller voxels first the shafts would be assigned . The shafts in this case includes the vertical circulation elements like the stairwell and the elevators as well as the buildings services shafts. The horizontal shafts would include the circulation passages connecting the various spaces in the building.The approach taken towards assigning the shafts depends on the `path-space relationship` for the horizontal shafts and the `base shape` for the vertical shafts.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Path_Space_relationships-01.png" >}}
Path-Space Relationship diagrams.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Horizontal%20Shafts%20buiksloterham.jpg" >}}
Shaft assignment done in the model.


`Step3:`Assigning Green Spaces:
The assignment of green spaces depending on the shape of the Zones and the units needs to be done. The location of Green spaces has the potential to elevate the spatial quality of the units and the zones around it.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Green_Spaces_buiksloterham.jpg" >}}
The green zones are assigned at intersections of zones.

`Step4:`Assigning the first category of Units:
The first category of units are the ones without any closeness requirements or relations. These include all the housing zones in the space program and the zoning output which will be assigned first.


`Step4:` Assigning the Second category of Units:
The Second category of the units include the ones having closeness requirements with other units in the zone. The units for the office zone the restaurant zone lie under this category. The assignment of these units will be formulated like the zoning problem.

## Steps involved in assigning the first category of Units:
In the first category of units all the units under the residential function are assigned. This includes Privately owned housing, Social-sector Rental Housing, and Free-sector Rental Housing.The unit assignment process for this category will be explained by considering the example for the privately owned housing units.

`Step1:` Generating the modules for units:
The privately owned housing units have two categories as seen in the Large house consisting of 18 voxels and the medium house consisting of 9 voxels. The zone for the privately owned housing is split in the center by the horizontal circulation space in the previous step and is symmetrical with one side containing a maximum of 3 voxels. Considering this dimension as the extent for each unit since intermediate units are not desirable due to poor access to the sun the units for the large and the medium can have a shape of 3x6 voxels and 3x3 voxels respectively. 

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Units-02.png" >}}
Basic Units.

`Step2:` Generating the intermediate modules:
The counting of the voxels is done in each direction for the two symmetrical sections of the zone. One dimension is the same being 3 voxels but the other dimension will keep on varying. This variation in the other dimension will lead to instances where the dimension is not divisible by three which is the minumum size of the unit (Medium house). For these specific instances intermediate scaled units need to be designed. In the shape for the privately owned housing two such intermediate unit types need to be made of sizes 4x3 voxels and 5x3 voxels respectively. 

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Units-03.png" >}}
Intermediate Units.

`Step3:` Assigning the modules according to the desirability matrix:
Once all the types of units are made the assignment process starts. The Large houses are given a priority and are assigned first sequentially floor after floor starting from the top floor since the maximum values from the desirability matrix as seen in the zoning problem for the privately owned housing were at the top of the lattice. [Privately owned housing output lattice](/posts/zoning-problem-MCDA). At the end of each floor the intermediate modules are assigned if the length is not perfectly divisible by three. 
This process is repeated for the other two type of housing units, thus concluding the unit assignment process of the first category

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment_cover.gif" >}}

## Steps involved in assigning the Second category of Units:
The second category of units are the ones having closeness requirements with each other. An example of this is the zone for Offices and the restaurants and retails zones. To show the method the offices zone will be considered. The approach taken will be similar to the agent based method taken for the zoning problem with an added contraint of closeness.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Zoning_problem_Diagram.jpg" >}}
Diagram showing the office zones.

`Step1:` Generating the REL-CHART: 
The relationship chart indicating the closeness between the units in the problem needs to be established first. This will indicate the constraints for the agent orgin locations in the model further. In this approach the Total closeness rating is considered which is an aggregated value of the closeness ratings for each zones as seen in the table below. According to this Total closeness rating the agents will be deployed.
For the Office zones there are two distinctions made between `Co-working` offices with a suffix `Common` and `Privately Owned` offices with a suffix `Private ` in the Rel-Chart below :

| REL_CHART | Open Office Area Private | Cafeteria Private | Meeting Rooms Private | Open Office Area Common | Meeting Rooms Common | Cafeteria Common | TCR |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Open Office Area Private | nil | 4 | 3 | -1 | -1 | -1 | 4 |
| Cafeteria Private  | 4 | nil | 2 | -1 | -1 | 3 | 3 |
| Meeting Rooms Private | 0 | 2 | nil | -1 | -1 | -1 | -1 |
| Open Office Area Common | -1 | -1 | -1 | nil | 3 | 4 | 4 |
| Open Office Area Common | -1 | -1 | -1 | 0 | nil | 2 | -1 |
| Cafeteria Common | -1 | -1 | 1 | 4 | 0 | nil | 3 |

Where:(4)Absolutely Necessary, E:(3)Especially Important, I:(2)Important, O:(0)Ordinary closeness, U:(1)Unnecessary closeness, X:(-1)Avoid closeness

`Step2:` Developing the Spatial Quality matrices for the zone: 
In the following steps the necessary matrices for the Agent based simulations will be done as seen in the Zoning problem beginning with generating the Spatial Quality matrices or enviornment matrices in the same manner as seen in [Enviornment lattices](/posts/zoning-problem-enviornment). The additional spatial quality indicator is the closeness to the green areas done for locating the common spaces in the units. 

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Closeness_to_grren_Areas_viz.png" >}}
Closeness to Green area lattice, where the points highlight the location of green spaces nearest to the Office zone.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Distance_from_Roof.png" >}}
Distance based lattices (Distance from Ground level)

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Quiteness_lattice.png" >}}
Distance based lattices (Distance from Noise source)

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Solar_lattice_zeroed.png" >}}
Intersection based lattices (Sun-Access Lattice)

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Visibility_to_IJ.png" >}}
Intersection based lattices (Visibility_Lattice)

`Step3:` Developing the Desirability matrices for the agents: 
In order to generate the desirability matrices for the agents the decision making will be done regarding the spatial qualities necessary for the various units inside the office zone similar to the step taken in the zoning problem [Desirability lattices](/posts/zoning-problem-MCDA).Once decisions are made a MCDA process will run based on the decision and a series of desitrability lattices will be produced which will act as the base for the agent simulation in the further steps. The choices done for the units can be seen in the table and images below:

| Spatial Quality | Open Office Area Private | Cafeteria Private | Meeting Rooms Private | Open Office Area Common | Meeting Rooms Common | Cafeteria Common |
| :-: | :-: | :-: | :-: | :-: | :-: |
| Closeness to N facade | 0 | 0 | 0 | 0 | 0 | 0 |
|  Closeness to S facade | 0 | 0 | 0 | 0 | 0 | 0 |
| Closeness to E facade  | 0 | 0 | 0 | 0 | 0 | 0 |
| Closeness to W facade | 0 | 0 | 0 | 0 | 5 | 0 |
|  Closeness to Ground | 7 | 0 | 0 | 0 | 0 | 0 |
|  Closeness to Roof  | 0 | 0 | 8 | 0 | 8 | 0 |
|  Closeness to Green Areas  | 0 | 8 | 0 | 0 | 0 | 8 |
|  Quiteness Lattice  | 6 | 0 | 8 | 0 | 0 | 0 |
|  Sun Access Lattice  | 7 | 0 | 7 | 0 | 7 | 0 |
|  Visibility to IJ Lattice  | 0 | 4 | 7 | 0 | 7 | 4 |
|  Visibility to Road  Lattice  | 6 | 0 | 0 | 0 | 0 | 0 |

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Meeting_Rooms_Private%20(1).png" >}}
Desirability lattices for the Meeting Rooms Private units

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Cafeteria_and_Common_rooms_Private%20(1).png" >}}
Desirability lattices for the Common Rooms Private units

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment/Open_Office_Common%20(1).png" >}}
Desirability lattices for the Open Office Private units


`Step4:` Run the Agent based simulations to develop the units: 
The process ismilar to the [Sequential assignment](/posts/zoning-problem) process will be done to assign the units inside the office sones. The cuboidal occupy behaviour for the agents will be considered and the sequence orf the agents will depend on the Total closeness rating for the units as derived in step 1 of the process. 
For spatial relations with strict closeness relations like highly desirable or avoid strict constraints will be enforced on the agent origin positions based on the size of the units that the agent is attempting to grow. 

{{< youtube id="iikMRGpqEE0" autoplay="true" >}}

Finally the oputput from the Unit assignment problem will be further processed in the [Unit-Layout problem](/posts/unit-layout-problem)
{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Zoning_problem_to_unit_assignment_problem.png" >}}