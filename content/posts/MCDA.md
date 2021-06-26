---
title: Multi-criteria decision analysis
date: "2021-06-05"
tags:
  - Multi-criteria Decision analysis

keywords:
  - architectural design
  - decision theory 

description: The process and theory behind the Multi-criteria decion analysis done in the various nested levels of configuration problem.
showFullContent: false
---
# MCDA

The problem of generating optimal Architectural configuration is a complex one where many decisions have to be taken simultaneously to achieve the configuration goals by multiple stakeholders.The process implemented in the thesis is a methodical one where the multi-dimensional, multi-criteria, multi-actor complexity of decision making in a large problem is divided into smaller ordered logical steps and at each step a set of decision variables is defined and the process of MCDA is applied.

The process of MCDA is capable of solving a decision making problem which has conflicting criteria and weights. The selection of appropriate method for MCDA is crucial for generation of the desired results for the decision making problem. [Watrobski(2019)](https://www.sciencedirect.com/science/article/pii/S0305048317308563) in his paper has described a method to build a formal guideline for MCDA method selection, which is independent of the problem domain and has published a free to use [tool](http://mcda.it/)for the public  to choose an appropriate MCDA method.The tool was used to select a MCDA method by defining the abilities of the method.

The following details were added to find the _MCDA method [has weights, Weights type(quantity),Scale(quantity),Has uncertainty(no uncertainty),Topic(ranking and choice)]_.When the problem of configuration was analysed in the program results from the tool indicated that `TOPSIS`could be a method which can be used to solve this MCDA problem. TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution) is a multi-criteria decision making technique used to rank a finite set of alternatives based on the minimization of distance from an ideal point and the maximization of distance from an anti-ideal point . The normalization step in the method can help in comparing values which have different range and scale and units which is especially beneficial when comparing different environmental simulation values.

This method was also selected as the preferred method since it could solve the problem and was easily available as a Python library.The [Scikit criteria](https://scikit-criteria.readthedocs.io/en/latest/index.html) python library was used to process the performance data and the user preferences to score and rank the Design variant options.The interactive HTML widgets for jupyter notebooks were used to record the user preferences for the performance indicators.

{{< image src="https://raw.githubusercontent.com/adityasoman/GEN-ARCH/main/Website/Massing_problem/TOPSIS_result_massing.jpg" >}}

An example of TOPSIS method used for ranking the design variants from the massing problem.
