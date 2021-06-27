---
title: The Layout problem
date: "2021-06-09"
tags:
  - architecture
  - zoning
keywords:
  - architecture
  - computation
cover: ../Images/Stakeholders-04.png
description: This article explains the complexities of the 3D Layout problem 
showFullContent: false
---
# The 3D Layout Problem

The problem of 3D layout configuration, when regarded in its full sophistication, is a classical example of a wicked problem that is at the same time a complex combinatorial problem which can be classified as a NP-hard problem , and arguably the most difficult problem of computational design for which the level of ‘control’ provided by the claimed methods in the literature is limited.This is majorly because of the Human Physical complexities involved. Reaching a consesus among the actors itself is very difficult because of contrasting ideas and focus points of the actors about the configuration.


In this thesis an attempt is made to systematically separate the process of 3D layout configuration as a series of steps with local goals and with a certain set of assumptions and simplifications to achieve the global spatial planning goals. In the following section each level of problem will be elaborated further with the stakeholders(actor) involvement in them the detailed mathematical formulation and the method used will be elaborated further in the report.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Consessus%20Diagram.png" >}}

`Massing problem:`
The highest nesting level of problem is the massing problem.As a first step toward solving the problem a volumetric representation of the building needs to be generated. In architectural practise it is common to sketch out various design options for the project on a conceptual level using representative 3d blocks having a low resolution of details. In this stage of the design process Architects, Developers, Governing authorities like Municipal corporations are the main stakeholders involved. The goals for the  Architects is develop their concepts on the brief provided by the Developers. The goal of Developers is to maximise the profit or the developable area on the site and the goal of the Governing bodies is to assess the impact of the development on the immediate surroundings and the city and to safeguard the rights of the citizens of the block.


In this thesis the massing problem is solved by means of a combination of manual design and digital validation. The process taken in the massing problem is a series of systematic steps and decisions to generate and validate the design options. Generation of the massing blocks at each stage is done manually in a 3D modelling environment of Rhinoceros and the validation part is done partly on Grasshopper for simulations and python for processing the simulation data and creating a validation framework. The main reason for this approach is not to restrict the freedom of design involved in the initial phase of the design project but to generate feedback on the designs for a better development of the overall proposal.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Massing_to_zoning.png" >}}

`Zoning problem:`
In the selected massing option locating the appropriate zones is the main goal of the zoning problem. Based on the space program zones are defined and their requirements are also determined. The zoning requirements have two main characteristics. The first one being the closeness relation with other zones and the second one being the performance score of the zone as defined by the stakeholder decisions. The stakeholders and their goals for the zoning problem are as follows:

The architect will make a framework for all the rest of the stakeholders to participate. The framework the decisions available to each stakeholder will be mentioned and the feedback for of the stakeholders will also be taken for any additional requirements. Once the preferences and decisions of other stakeholders are recorded the architects evaluates the preferences of all the stakeholders and  makes a combined decision model which will guide the zoning goals of the project. The performance of the zoning will be assessed on how close the zones are placed to the ideal location for the zone. Several methods were explored to solve the zoning problem among them the main one is a multi-agent system to generate the zoning clusters.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Zoning_problem_to_unit_assignment_problem.png" >}}

`Unit assignment problem:`
In the selected zoning model of the building assigning the units is the main goal of this problem. Units can be defined as the higher level function or cluster of rooms defining a function. For example in a residential building an apartment is a unit of the space program.
The first step before the assignment process is to generate the circulation shafts in the zoning model. The vertical circulation shaft containing stairwells elevators and building services ducting is first located by analysing the zoning model and the geometrical properties of the massing. The horizontal circulation elements can be added after this step or later after the unit assignment is done depending on the quality of circulation that the user picks. If for example the circulation is through the spaces then it can be assigned after the units are placed but if the spaces are along the circulation then the horizontal shafts have to be assigned after the vertical ones.
The Architect and the Developer are the main stakeholders in the unit assignment goals. The main goal of the assigning is to generate good clean floor plans with optimal use of the floor area and a good access to daylight respecting the area bounds given by the developer for each unit. 

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_assignment_problem_to_Unit_Layout_Problem.png" >}}
        
`Unit layout problem:`
In the unit layout problem the main goal is to generate the infill needed for the occupants of the units.The internal room layout for the unit is generated in this step. The stakeholders involved in this step is the end user and the architect. The end user first records the preferences with respect to the number of rooms and their placement and the architect feeds it into the tool. The tool will generate multiple layout which fits the goals of the end user and  the end user can approve the layout or change the preferences for an improved version. After a final layout is made the detailing aspect of the project is recorded. This problem of generating layouts according to user preferences without compromising the layouts of other users is quite tedious and time consuming as seen in the various case studies before in the [literature review](/posts/open-buildings).An automated process for this which develops floor plan options based on the user preferences and complying with the rules set by the architect would be very useful.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Unit_Layout_Problem_to_unit_detailing_problem.png" >}}

`Unit Detailing problem:`
The Unit detailing problem is the next step after the Unit layout problem. The main goal of this step is to specify the infill details which are defined in the unit layout stage. The end user along with the architect will decide on the materiality of the infill elements where the end user can pick elements from the catalogue defined by the architect. The tool at this stage will give output by the means of a dashboard with various indicators for the end-user to understand the financial, sustainability and spatial aspects of the choices made. based on looking at the output of the Dashboard the user can keep on changing the choices till an desired outcome is generated. The catalogue will be developed by the Architect in collaboration with the Building Product manufacturers and Building contractors for maintaining accuracy in the details of it


The computational design methods used in solving the problems take inspiration form a lot of disciplines in solving similar problems as seen in the figure below:
{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Architectural_configuration.png" >}}