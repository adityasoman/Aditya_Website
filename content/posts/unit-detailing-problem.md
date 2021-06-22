---
title: 05 Unit Detailing Problem
date: "2021-06-01"
tags:
  - architecture
  - zoning
keywords:
  - architecture
  - computation
cover: ../Images/Unit_Detailing.gif
description: Finding the appropriate volumetric design of the building
showFullContent: false
---
# Unit Detailing problem

The Unit detailing problem deals with generation of design details for the units developed in the unit layout problem. Design details may consists of the following things. Materials and components of the various infill layers in the unit like Walls, Windows, facades, floors, ceilings, installations, furniture's etc. The clear distinction between the structure and infill has been made in the open building concept and the infill layer is the main element which will be detailed in the unit detailing problem. The structure layer should ideally be resolved in the unit assignment problem itself so at this stage there is already information regarding the structure of the building

The stakeholders involved in this stage of the layout problem are the Architects, Contractors, End users of the space/ Home-owners, Building Component manufacturers. The system created for solving this problem would make the Architect/ Designer as the mediator between the end user and the rest of the stakeholder generating the necessary inputs for the communication.

The nature of the problem at this stage will involve background knowledge about a lot of subjects like construction processes, building material properties, fabrication and construction processes etc. This makes the scale of the problem very large so the approach presented in this article is a brief overview.

# Aim

To genrate the infill details for the Layouts developed in the unit layout stage in terms of materiality and design detail.

# Proposed Configuration process

A feedback loop is essential for this stage of the configuration problem. The feedback can consist of various things like building costs, material passport, material details and quantities, circularity index etc. This will ensure that the user knows the impact of the selection decisions on the project.
Generation of 3d blocks which can store this information while displaying the final result visually will help in the design process. The approach of creating the 3d blocks is similar to BIM modelling where details of all the components are mentioned while creating families and blocks. Two kind of approaches can be taken to assign the created blocks into the floor layout. The automatic assignment approach and the manual one.

In the automatic layout assignment approach the details for the rooms in the unit will be recorded from the participants or the end users and the necessary 3d blocks with the information will be first created by the architect in consultation with the rest of the stakeholders. The user will be given a choice between the materials for each category of components like the walls , floors, etc and the result of the selection will be shown in the feedback loop. The selection will not only be based on material but on boundary conditions as well like internal walls, room wise details, edge of wet areas and dry areas, facades etc. Once all the details are recorded based on the boundary conditions defined the blocks will be assigned automatically. Whereas in the manual process the user will be able to see and assign the created blocks in the floor layout to the specific voxels in a tactile game like manner. The creation of the 3d blocks is something similar to the reference of the game [Block-hood](https://www.plethora-project.com/blockhood) where assigning the blocks generates a feedback about the resources utilized and the assignment process itself is based on certain adjacency conditions.

{{< image src="https://images.squarespace-cdn.com/content/v1/582f98dbb3db2be72dc14252/1496268505965-F3G3PG6KEM4FH74YP57N/ke17ZwdGBToddI8pDm48kPTrHXgsMrSIMwe6YW3w1AZ7gQa3H78H3Y0txjaiv_0fDoOvxcdMmMKkDsyUqMSsMWxHk725yiiHCCLfrh8O1z4YTzHvnKhyp6Da-NYroOW3ZGjoBKy3azqku80C789l0k5fwC0WRNFJBIXiBeNI5fKTrY37saURwPBw8fO2esROAxn-RKSrlQamlL27g22X2A/image-asset.jpeg?format=1000w" >}}
[Block-hood](https://www.plethora-project.com/blockhood) game imagery.

# Steps involved in the configuration aproach
In the configuration approach for the unit detailing problem there will be a distinction made between the objects and the infill layer. All the building elements will comprise under the infill layer and the furniture, appliances  will come under the object layer. The configuration problem stops at the infill level and the object level goes beyond the scope of the configuration problem.

The 3d block generation can happen in either two dimensional enviornment or a 3d enviornment. The two dimensional enviornment generally consists of single height  spaces and the 3d enviornment will consist of larger volumes and multi-story spaces. The minimum number of blocks which need to be defined to create a space vary for both the cases.A two dimensional case would be considered to illustrate the system for unit detailing. 
The following steps are taken to define the unit detailing:

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Detailing/Plan_to_Detail.png" >}}
From the selected Unit Layout to a voxelated output 


`Step1:` Initilization and Block creation:
As a first step a plan is selected from the unit layout problem stage for further developing in the unit detailing stage. The blocks are configured in the following manner: Every block will have flooring slab , flooring finish , Ceiling finish . There is a further option of creating a block with wall segment for internal walls and facade segment for external walls. The blocks with wall segment can be created either as a peripheral wall block or a central wall block. To create a set of blocks which will generate any type of an layout both the types of blocks are necessary. Furthermore in case of a block with wall the blocks need to be made with a single wall , with double wall for corner junctions for both the centrally placed walls as well as the peripheral walls. The walls themselves can have openings which can be plain empty openings, doors, and windows.The information regarding all of this can be stored in the voxel id as seen in the image below .

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Detailing/Voxel_Adjacency.png" >}}
The faces inside a voxel can be represented by indices and boolean values can indicate if its present or not. Each voxel in the layout will have the details embedded in it.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Detailing/All_Blocks-01.png
" >}}
ALl the blocks that were created for the Toy problem

`Step2:`Block information input:
Along with the creation of blocks the information stored in each one of the blocks also needs to be filled. The level of information depends on what kind of dashboards or feedback the stakeholders expect. The dashboard will keep on updating the necessary details when the blocks are assigned to inform the user about the selected performance parameters. Based on that the user can modify/ create new blocks for meeting the goals. 

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Detailing/Voxel_Details.png" >}}
Each voxel can have a information layer along with the geometry layer


`Step3:` Block Assignment:
The blocks are assigned in the voxelated grid either room by room or by simply enumerating through the array in row wise or column wise manner. The blocks are picked based on the location of the voxel in the floor plan. The voxels in the room clusters store information regarding their position (corner/intermediate/junction) and requirement like doors and windows based on which appropriate block is assigned. In the manual process the appropriate blocks can be selected manually and assigned. This concludes the unit-detailing process.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Detailing.gif" >}}
Unit Assignment based on the choices made by the user

