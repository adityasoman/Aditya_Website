---
title: 02 Zoning Problem
date: "2021-06-04"
tags:
  - 3D Layout problem
  - Zoning problem
  - Agent based modelling
keywords:
  - architecture
  - computation
cover: ../Images/zoning/Zoning_cover.gif
description: Designating the appropriate locations for the various functions in the space program clubbed under particular zones
showFullContent: false
---

# Zoning Problem

The zoning problem involves `generation` and `allocation `of zones inside a building mass which will cater to a specific function from the program of requirements of the building. There are two parts to the problem, the first one being the location of the zones and the closeness with respect to other zones and the second one is the shape and topological structure of the zones with respect to the island formation, connectivity and form. Generating a high performing zoning solution will involve balancing the two aspects of the problem.

Determining the appropriate location of zones is a complex problem in itself. It highly depends on the design choices made by the actors regarding the spatial qualities required from the zones. The desirability of a location for a zone in a building would involve generating a collective decision from all the choices made by the actors involved in the configuration process. Location of the zones however is also bound by constraints where the location of the zones with respect to other zones also needs to be considered for accessibility and connectivity, thus adding an extra layer of combinatorial complexity to the problem.

The level of control over the geometrical and topological resolution is the second part of the problem. Forming and shaping the best possible geometry according to the design intention while maintaining topological connectivity for the zones is essential and is a difficult task to manage when following the desirability results regarding the location of the zones. The main actor (architect) in this particular level of the problem needs to define the rules for growth of the zones which will generate the intended spatial quality of the zones to ensure the validity of the design solution.

The concept of `multi-agent systems` is used to solve the zoning problem.The multi agent system tries to achieve the global and local goals of the zonal configuration like controllable generation of a spatial system consisting of routes pertaining to a graph with closeness weights, spatial zones fitting into locations fulfilling their requirements and fitting their performance goals, and the compactness of the entire system into a space-efficient mass by devising the rules and behaviours of the computational agents in a quest for emergent optimal configuration such as a termite mound. The computational agents effectively grow the design decision taken by their respective actors into a zoning solution.

# Aim

To assign and generate Zones in a discretized massing model which will achieve the maximum performance value in terms of gathering the most desirable voxels for each zone while maintaining the necessary closeness requirements as specified by the actor.

# Multi-Agent system

In the multi-agent system designed to solve the Zoning problem there are three main elements.
`1.Environment Lattices: `The [environment lattices](/posts/zoning-problem-enviornment) are developed by performing various environmental simulations on the discretised massing model or the voxel grid generated at the last stage of the massing problem.These enviornment simulations represent the spatial quality that the actor can choose while making design choices for the zones.

`2.Agent Performance criteria:` [Performance criteria](/posts/zoning-problem-mcda) are the lattices which are generated as a result of decision making with respect to the importance and need of the selected spatial qualities for the zones which the agent is trying to grow.

`3.Agent Behaviours:` [Agent behaviours](/posts/zoning-problem-agent-behaviours) are the actions which the agents can perform to achieve their goals on the performance criteria lattices to grow the zonesin the discretised massing model.

# Results

The results generated for the zoning problem using the multi-agent system described in the previous section are discussed in detail in this section.Since the massing model or the spatial model is discretized into voxels it is possible to make discrete decision making and the problem of zoning can be looked in the form of location allocation problem. Due to this conversion of the abstract architectural problem into a mathematical problem, research from other engineering disciplines like Operations research in industrial engineering can be considered as inspiration.
There were two approaches considered for growing the decision of the actors using the multi-agent system. The first one is the Linear assignment approach.

# Linear Assignment approach:

The first approach towards this problem is to deal with the zoning problem as an linear assignment problem researched extensively in operations research. The problem was first described by [Koopman](https://www.jstor.org/stable/1907742) as a relatively simple problem in the allocation of indivisible resources is that of matching two sets of an equal number n of objects, by making up pairs of objects consisting of one object from each set. Objects belonging to the same set are similar in kind but not identical. For each of the n<sup>2</sup> possible pairs a score or value is given. The problem is to find a matching (or assignment to each other) of objects for which the sum of the scores of pairs matched is as high as possible.

Considering the problem of zoning the objective of this same problem can be reinterpreted as maximising the summation of all the values of voxels in a cluster (function) for all clusters.

## Steps involved in the Linear Assignment approach:

`Step1:` Determine the possible agent origin locations
The smallest zone in the whole program is the Restaurant and Cafe Zone consisting of 19 voxels that need to be occupied. So Considering this as the benchmark for division of the occupancy lattice all the available cells were divided into clusters of 20 cells to find the positions for 71 possible origin points for the agents.The number of agents for each of the zone was also divided based on this smallest occupancy size of the zone as seen in the table below:

| Zones                      | Number of Voxels | Number of Agents |
| -------------------------- | :--------------: | :--------------: |
| Privately owned housing    |       451        |        21        |
| Social rental housing      |       301        |        16        |
| Free sector rental housing |       403        |        21        |
| Restaurants and cafe       |        19        |        1         |
| Retail Stores              |        73        |        4         |
| Offices                    |        93        |        5         |
| Parking                    |        51        |        3         |

So each agent in the table has the goal of occupying the best 20 voxels surrounding its origin position.The final output of this step is a list of possible origin locations.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Initial_Positions_agents.png" >}}

`Step2:` Generating the Benefit matrix for the Agents
The ABM simulation for all the position for all the agents is run in isolation and the total benefit generated by the occupying agents at each of the positions is recorded. The environment lattice which is the desirability lattice for the agent is also considered according to its zone. This simulation in isolation will give an idea about the benefit for the particular location for the twenty voxels which each agent has to occupy in the simulation. These recorded benefits are stored in a matrix as the output of this step.

`Step3:` Linear Assignment Process
The Benefit matrices for the agents are used in the MIP solver with SCIP backend of the [Google OR tools](https://developers.google.com/optimization) to formulate a linear assignment problem where 71 agents have to be assigned to 71 origin positions in the base lattice of the model. The solver runs the calculation and generates the permutation matrix for the assignment problem which acts as the output of this step.

`Step4:` Running the ABM Simulation according to the Permutation matrix
The permutation matrix is used to run the agent based simulation for all the agents and the total benefit of the whole simulation is calculated by aggregating the occupied values from the desirability matrices of all the agents to calculate the total benefit.

{{< youtube id="ny96xxiPR_g" autoplay="true" >}}

# Sequential Assignment approach:

In the sequential assignment approach the approach is more towards replicating the manual process with the intelligence of multi criteria assignment and form evolution offered by the agent based model.In this approach the functions in the space program are assigned sequentially from the biggest function to the smallest function. This approach gives priority according to the size assuming that the impact of the biggest function is going to be the most on the output of the benefit calculations of the zoning.

The similarity of the approach to the manual process can be attributed to the fact that in the manual process multiple zones are never assigned its always a sequential process with a explicit or an assumed priority order of the various zones. The main benefit of this approach is the topological quality of the zones created in terms of their shape and island formation. Since the growth of the agents is not affected by the growth of their surrounding agents the agents can grow in the exact way that they are programmed in response to the environment lattice values which they are fed with.The interesting thing to observe in this approach would be the final score of the simulation in comparison to the Linear assignment approach. In this type of an approach the lower the function or the agent is in the priority list the more it has to compromise in the quality of voxels which it can occupy. In that sense this approach does not give equal access to all the functions.

## Steps involved in the Sequential Assignment approach:

`Step1:` Determine the possible agent origin locations.
The first step in the sequential assignment procedure was to parse the base lattice and generate a good sample size for the agent origins. Out of the 1359 available voxels a voxel after every 10 voxels was considered in the list for possible agent origins. This kept the resolution for the simulation higher the intention being to generate more accurate results.

`Step2:`Separating the lattice into seperate buildings.
The graph seperation was done by using the connected components function from the library [networkX](https://networkx.org/) to separate the available voxels into individual separate building blocks. This would help in controlling the spread of the zones over all the building blocks.

`Step3:`Generating the Benefit matrix for the Agents.
This step is the same as the linear assignment approach second step where ABM simulation for all the position for all the agents is run in isolation and the total benefit generated by the occupying agents at each of the positions is recorded. The environment lattice which is the desirability lattice for the agent is also considered according to its zone.These recorded benefits are stored in a matrix as the output of this step.

`Step4:`Sequential Assignment Procedure.
The sequential assignment procedure is started at this step beginning with the parking and the Privately owned housing zones. The agent behaviour for parking was a 2d rectangular growth one and for the privately owned housing was 3d cuboidal one considering the nature of the spaces.The agents are initialized in Building one and Building four together to make the zone distributed over the two buildings.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Step_one_Sequential_Case.jpg" >}}
First step in assignment of Zones with parking in Blue and Privately owned housing in pink.

Once all the voxels for the agents are occupied then the availability of the remaining voxels are scanned for the best possible origin location for the next agent by comparing it with the list generated from step one of the process.Once a suitable origin is found the simulation is run again . This process continues till all the agents have occupied the desired number of voxels.
{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Step_two_Sequential_Case.jpg" >}}
Second step in assignment of Zones with Social rental housing zone displayed in Green

`Step5:`Generating the Total Benefit of the simulation.
Once all the agents have occupied the desired number of voxels the desirability values for each one of them are extracted from their respective desirability lattices. The aggregated value for each of the lattice is added to generate the total benefit of the assignment process.

{{< youtube id="iikMRGpqEE0" autoplay="true" >}}

# Comparison between the approaches:

The Linear assignment approach outperformed the Sequential assignment one substantially. The `Linear Assignment approach` output obtained the score of `7.18/10` and the output obtained from the `Sequential assignment approach` scored `4.35/10`. This can be attributed to the uniform divisions of the agent occupy goals for the linear assignment one where the influence of one agent growing over the other is reduced substantially and the MIP solver is able to predict accurate results.The sequential assignment method does not give equal access to all the agents to achieve their respective goals with preferences given to the agents assigned first. There are a few drawbacks with the linear assignment process as well.The main drawback of the linear assignment method is the formation of scattered unconnected smaller zones in the lattice. Since the only aim in this approach is to maximise the benefit the topology of the zones formed is not really considered. Isolated small clusters can be seen at a lot of places in the output which need to be consolidated.

# Conclusion and Limitations for the Zoning Problem:

The zoning problem is complex in its nature and the selection of the appropriate method is crucial in generating a solution for it. As a first step the nature of the problem needs to be identified in terms of its requirements related to the closeness between the zones. If there is a closeness requirement then the approaches mentioned in the TCR approach need to be considered and if here isn't a closeness requirement the sequential approach or the Linear assignment approach can be considered.The sequential assignment approach has an advantage in generating topologically well formed zones since there is no interference of the growth of other agents but it performs poorly when it comes to achieving the performance goals for each of the zones due to unequal access. The Linear assignment approach performs excellently in achieving the performance goals since it has a finer resolution for growth and scans the environment fields more accurately. However it may perform badly in terms of topological structure since generation of a single island is not under consideration in the method.

One of the biggest drawbacks or limitations in the whole Agent based method is the lack of communication between the agents while performing the behaviour. The whole requirement of an improvement step will be eliminated if the agents would communicate with each other before performing a behaviour against a voxels having shared interests. If this negotiation would happen during the simulation then the agents could grow in the topological form that they were programmed to grow into not affected by the growth of the other agents.

One of the avenues which could be explored to generate good combinations is the use of evolutionary algorithms to search for a suitable permutation matrix for the agent origins. Since the nature of the growth of one agent affecting the other is not easily predictable.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Step_two_Sequential_Case.jpg" >}}
The final output for the zoning has a voxel dimensions of 6x6x6m which is interpolated into a finer resolution of 3x3x3m for the [Unit Assignment problem](/posts/unit-assignment-problem) using the components from the Scipy Library.

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Zoning_problem_to_unit_assignment_problem.png" >}}
