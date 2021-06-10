---
title: 02 Zoning Problem
date: "2021-06-06"
tags:
  - 3D Layout problem
  - Zoning problem
keywords:
  - architecture
  - computation
cover: ../Images/Zoning_problem_Cover.png
description: Designating the appropriate locations for the various functions in the space program clubbed under particular zones
showFullContent: false
---
# Zoning Problem

The zoning problem deals with designating the appropriate locations for the various functions in the space program clubbed under particular zones. Two things are primarily important while assigning the zones the closeness requirements of the zones with respect to each other and the appropriateness of the zones w.r.t to the decisions taken by the architect regarding the desired performance criteria.

The concept of `multi-agent systems` is used to solve the zoning problem.The system tries to achieve the global and local goals of the zonal configuration like controllable generation of a spatial system consisting of routes pertaining to a graph with closeness weights, spatial zones fitting into locations fulfilling their requirements and fitting their performance goals, and the compactness of the entire system into a space-efficient mass by devising the rules and behaviours of the agents in a quest for emergent optimal configuration such as a termite mound. Choosing a multi agent system over other techniques is done due to the transparency and adaptability of the method to search for valid options in the massive combinatorial search space along with didactic reasons.

# Aim

To assign Zones in a massing model which will achieve the maximum performance value and the necessary closeness requirements as specified by the stakeholder.

# Multi-Agent system

In the multi-agent system designed to solve the Zoning problem there are three main elements.
`1.Environment Lattices: `The [environment lattices](/posts/zoning-problem-enviornment) are developed by performing various environmental simulations on the discretised massing model or the voxel grid generated at the last stage of the massing problem.

`2.Agent Performance criteria:` [Performance criteria](/posts/zoning-problem-MCDA) are the lattices which are generated as a result of decision making with respect to the importance and need of the selected simulation matrices for the agent.

`3.Agent Behaviours:` [Agent behaviours](/posts/zoning-problem-Agent-behaviours) are the actions which the agents can perform to achieve their goals on the performance criteria lattices.
