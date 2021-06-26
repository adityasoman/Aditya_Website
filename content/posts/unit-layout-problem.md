---
title: 04 Unit Layout Problem
date: "2021-05-29"
tags:
  - architecture
  - zoning
keywords:
  - architecture
  - computation
cover: ../Images/Unit_Layout.gif
description: Finding the appropriate volumetric design of the building
showFullContent: false
---

# Unit Layout Problem

The Unit layout problem deals with the generation of layout for individual units as defined in the unit assignment problem. The unit layout is highly dependent on the use case scenario of the space so the interaction and the participation of the user of the space is extremely important at this stage.

# Aim

The main aim of this level of configuration problem is the generation of unit layouts based on the spatial choices and preferences of the final end user of the space along with respecting the design intention of the architect.

# Configuration Approach

The configuration approach that is proposed for the Unit layout problem resembles the Rectangle packing problem in computer science again inspired from the problem in the domain of operation research in industrial design . The rectangular packing problem in its full sophistication is a NP hard problem and become a very complex when the rotation and the sizes of the rectangles inside the in rectangle are made variable.

The approach proposed works on simplifications which make it a feasible problem to solve. The simplifications are methodical steps which are based on strong logic and can be modified or deleted according to the participants requirement. This makes the approach flexible and transparent for adaptation to various design styles and requirements. The unit layout configuration for a small unit of size 9x6m is considered as a test case or a toy problem and the following steps are followed:

# Steps followed in the procedure

`Step1:`Initial User preference/participant input:
The participants or the end users of the house are given a list of preferences that they have to input based on their requirements. The following inputs need to be specifed for the system to generate the design options for the participants:

The users have to define **how many rooms** they will be needing in the house and their details. The details include the **function** of the room and the requirement of **closeness to a service shaft**. Which will be determined by the function of the room like for example a bathroom or a kitchen. The second preference which the users need to specify is the requirement of **direct access to the facade / sunlight / ventilation** for the rooms. In these two preferences the maximum number which the user can define will be determined by the the Architect based for the dimensions of the unit and the ergonomic/ proportions which fit in the design vision. For the toy problem the following requirements will be considered :

Number of Rooms = 4

| Room Name   | Access to Facade | Access to Shaft |
| ----------- | :--------------- | :-------------: |
| Living Room | 1                |        0        |
| Bedroom     | 1                |        0        |
| Kitchen     | 1                |        1        |
| Toilet      | 0                |        1        |

1=True and 0=Flase

`Step2:`Initial master inputs:
The Architect or the designer is the controller of the process and needs to generate the following inputs for the system to initialize. The first one being the **maximum number of rooms that can have direct access to the facade.** This can be determined by the **minimum dimensions** of the room and the **dimensions of the facade.** The second input which the architect has to give is the **maximum and the minimum room sizes** for the possible rooms which the users can define. This is based on ergonomic principles of fitting the right furniture inside and the proportions which are comfortable for the occupants. Finally the architect also has to select the **location for the Vertical service shaft** which will carry all the ducting necessary for ventilation, plumbing , fire-fighting into the unit. In open buildings locating the shaft centrally is very important for maintaining the flexibility of the layout. This approach is inspired by the Superlofts project mentioned in the [literature review.](/posts/open-buildings)

Shape of the Unit = 9mx6m.
Maximum rooms on the facade = 9/3 = 3Rooms

| Room Name   | Min Size(m) | Max size(m) |
| ----------- | :---------- | :---------: |
| Living Room | 3           |      6      |
| Bedroom     | 3           |      6      |
| Kitchen     | 3           |      4      |
| Toilet      | 2           |      3      |

Initial master input by the Architect

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_one.png" >}}
Initial layout of the unit

`Step3:`Generation of Base blocks:
The initialization process is completed at step two so all the necessary input for the floor plan generation is ready. In this step the base blocks for all the spaces is initialized and enumerated. The base block considered for each room is the minimum size of the room which is needed. The enumerated options for the base blocks can be seen in the image below. The options for the Toilet block to be placed on the left /right side of the service block is also explored with the enumerations.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_two.png" >}}
Base block initialization for the units

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_two.gif" >}}
Base block enumeration

`Step4:`Distribution of remaining voxels:
After all the possible options are enumerated for the base blocks the question for distribution of remaining voxels is tackled. The total number of voxels in the base grid is 9x6 = 54 voxels, when subracted with the base blocks the number of voxels which are unassigned are 23 cells. These 23 cells have to be distributed among the 4 rooms in all possible ways. At this stage a constraint is added that the shape of the rooms should remain **largely rectangular** which means that at a time the cells corresponding to the minimum size for the room have to be added to the base block. This constrained coupled with the maximum possibility of having 3 rooms on the facade and the requirement of 3 rooms connected to the facade reduces the search space considerably. The possible floor plans because of this is around 7x4 = 28 floor plans. The base enumeration results in 7 options and the added options are based in the possible enumerations of toilet sizes and locations on either the left or the right side

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_three.png" >}}
Distribution of remaining voxels for the rooms in the unit

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_three.gif" >}}
Distribution of remaining voxels enumerations

`Step5:`Creation of Passages in the Layout:
Passages can be created to create more layout options and to improve the connectivity of the enumerated layouts in the step 4. Passages Can be created by specifying the path start and the end voxel and the shortest path can be created using the same method as described in the unit assignment problem horizontal shaft creation.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_four.png" >}}
Creation of passages in the units.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_four.gif" >}}
Creation of passages in the units enumeration.

`Alternative Design criteria:`
The layout possibilities become more interesting if the requirement of the rooms needing direct access to the facade is reduced . If the Toy problem is modified where the Kitchen no longer needs access to the facade the possibilities will increase considerably. The enumeration possibilities can be determined by creating a possible shape options for the rooms based on the minimum and the maximum sizes as shown in the table below:

| Living Room | Bedroom | Kitchen | Toilet |
| :---------: | :-----: | :-----: | :----: |
|     3x3     |   3x3   |   3x3   |  2x2   |
|     3x4     |   3x4   |   3x4   |  3x2   |
|     3x5     |   3x5   |   3x5   |  3x3   |
|     3x6     |   3x6   |   4x3   |        |
|     4x4     |   4x4   |   4x4   |        |
|     4x5     |   4x5   |   4x5   |        |
|     4x6     |   4x6   |   5x5   |        |
|     5x5     |   5x5   |         |        |
|     5x6     |   5x6   |         |        |
|     6x6     |   6x6   |         |        |

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_five.png" >}}
Alternative Design Possibilities.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout/Step_five.gif" >}}
Alternative Design Possibilities.

The enumerations because of this process can be seen in the last part of the image where the dimension of the room vary in X axis as well

`Step6:` MCDA and filtration:
Once all the possible layouts are generated based on the initial requirements the participants are given further choices like ordering the rooms based on their desired size, flow of the apartment in terms of which space comes first when you enter and the circulation distribution if the circulation in the apartment is central / linear (left oriented / right oriented). Finally the participants can select and give weights to these criteria. Based on the choices the calculations are done for all the layouts and a TOPSIS based MCDM model is developed for ranking all the layout options for the participants. The participants can choose between the options and the selected option will be further developed in the unit detailing problem. The [MCDM](/posts/mcda) is done to sort the layouts based on preferences of the participants which makes the selection process easier for them.

# Conclusions and Limitations:

The approach proposed in the thesis offers a controllable generation of the unit layouts and the level of control can be increased or decreased based on the number of constraints and simplifications which are done to the rectangular assignment procedure. This process seems to work well for housing kind of layouts but for other types of layouts the constraints might not be enough. For example in programs where there is a closeness requirements between the rooms this process will not work there is a need of an additional constraint of closeness. This method is similar to the brute force method with constraints to limit the options and the time required and is bound by its limitation. The space splitting method or the Physically based method where the spaces are represented by 2d bubbles and forces are applied based on the closeness requirements to generate the layout or the space splitting method where the data tree principles like Kd-trees are used to organise the floor plans could also be explored since they have proven to generate good quality 2d layouts in fixed boundaries as seen in the literature.

Alternatively the participants can be given a minecraft like game setting where they can do the assignment process of the rooms themselves to get familiarised with the process and get a better understanding of the participation process.The final out of this step is the selected high resolution voxelated layout showing the room placement inside the unit for the next step which is the unit detailing stage

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout_Problem_to_unit_detailing_problem.png" >}}
