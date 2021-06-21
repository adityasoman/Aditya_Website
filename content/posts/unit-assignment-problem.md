---
title: 03 Unit Assignment Problem
date: "2021-06-02"
tags:
  - architecture
  - zoning
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

## Steps involved in the Unit Assignment problem:
`Step1:` Interpolation of the Zoning problem output:
The first step in the Unit assignment problem is to make the resolution of the voxelated grid finer from a 6x6x6m size to a 3x3x3m size. This finer resolution will make assigning the units more accurate due to the smaller division size of the area into voxels.


