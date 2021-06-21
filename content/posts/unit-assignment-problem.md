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
| - | :-: | :-: |
| Privately owned housing | Large House | 60% of Zone Volume | 18 |
| Social rental housing | 301 | 16 |
| Free sector rental housing | 403 | 21 |
| Restaurants and cafe | 19 | 1 |
| Retail Stores | 73 | 4 |
| Offices| 93 | 5 |
| Parking| 51 | 3 |

## Steps involved in the Unit Assignment problem:
`Step1:` Interpolation of the Zoning problem output:
The first step in the Unit assignment problem is to make the resolution of the voxelated grid finer from a 6x6x6m size to a 3x3x3m size. This finer resolution will make assigning the units more accurate due to the smaller division size of the area into voxels.

`Step2:`Assigning Vertical and Horizontal Shafts:
In the base lattice consisting of zones and a high resolution lattice with smaller voxels first the shafts would be assigned . The shafts in this case includes the vertical circulation elements like the stairwell and the elevators as well as the buildings services shafts. The horizontal shafts would include the circulation passages connecting the various spaces in the building.The approach taken towards assigning the shafts depends on the `path-space relationship` for the horizontal shafts and the `base shape` for the vertical shafts.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Step_one_Sequential_Case.jpg" >}}
Path-Space Relationship diagrams.

`Step3:`Assigning Green Spaces:
The assignment of green spaces depending on the shape of the Zones and the units needs to be done. The location of Green spaces has the potential to elevate the spatial quality of the units and the zones around it.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Step_one_Sequential_Case.jpg" >}}
FThe green zones are assigned at intersections of zones.

`Step4:`Assigning the first category of Units:
The first category of units are the ones without any closeness requirements or relations. These include all the housing zones in the space program and the zoning output which will be assigned first.


`Step4:` Assigning the Second category of Units:
The Second category of the units include the ones having closeness requirements with other units in the zone. The units for the office zone the restaurant zone lie under this category. The assignment of these units will be formulated like the zoning problem.

## Steps involved in assigning the first category of Units:
In the first category of units all the units under the residential function are assigned. This includes Privately owned housing, Social-sector Rental Housing, and Free-sector Rental Housing.The unit assignment process for this category will be explained by considering the example for the privately owned housing units.

`Step1:` Generating the modules for units:
The privately owned housing units have two categories as seen in the Large house consisting of 18 voxels and the medium house consisting of 9 voxels. The zone for the privately owned housing is split in the center by the horizontal circulation space in the previous step and is symmetrical with one side containing a maximum of 3 voxels. Considering this dimension as the extent for each unit since intermediate units are not desirable due to poor access to the sun the units for the large and the medium can have a shape of 3x6 voxels and 3x3 voxels respectively. 



## Steps involved in assigning the Second category of Units:
