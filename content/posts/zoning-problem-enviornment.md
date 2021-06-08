---
title: 02 Zoning Problem - Enviornmental Simulations
date: "2021-06-1"
tags:
  - architecture
  - zoning
keywords:
  - architecture
  - computation
description: Designating the appropriate locations for the various functions in the space program clubbed under particular zones
showFullContent: false
---
# Enviornment Simulation Lattices

The simulations which were performed were based on the specific case considered in the project. The idea at this stage is not to generate a highly accurate simulation models, but simulations which are good enough for decision making. The generation of highly accurate simulations is also not possible at this stage since the material properties and the geometry of the various building elements is not defined yet.

The simulations are broadly divided into two types. The first one is based on finding `Eucledian distances` and the second one is based on `Ray obstruction` .


# Base voxelization

The initial step before calculations of simulation lattices was to separate the 4 masses into separate lattices for generating values locally for the individual masses. The voxelated lattice of the massing as derived from Massing Problem is a numpy n-dimensional array consisting of ones and zeroes. Ones represents the voxels inside the 3d object which are available for occupation and zero represents the exterior voxels which are not relevant to the simulations.The pseudo-code for voxelation is as follows.

```python
import os
import topogenesis as tg
import pyvista as pv
import trimesh as tm
import numpy as np

# Input Mesh

# load the mesh from file
mesh = tm.load(mesh_path)
# Check if the mesh is watertight
print(mesh.is_watertight)

# convert trimesh to pv_mesh
def tri_to_pv(tri_mesh):
    faces = np.pad(tri_mesh.faces, ((0, 0),(1,0)), 'constant', constant_values=3)
    pv_mesh = pv.PolyData(tri_mesh.vertices, faces)
    return pv_mesh

#Voxelize the mesh 

# initialize the base lattice
base_lattice = tg.lattice(mesh.bounds, unit=unit, default_value=1, dtype=int)

# check which voxel centroids is inside the mesh
interior_condition = mesh.contains(base_lattice.centroids)

# reshape the interior condition to the shape of the base_lattice
interior_array = interior_condition.reshape(base_lattice.shape)

# convert the interior array into a lattice
interior_lattice = tg.to_lattice(interior_array, base_lattice.minbound, base_lattice.unit)

# Save to Csv
csv_path = os.path.relpath('voxelized_envelope_6m_voxel_size.csv')
interior_lattice.to_csv(csv_path)


```

The binder link to the code [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/adityasoman/GEN-ARCH_Binder/a96f583c4cbf7c3058c9708c0849c99f37e1c718?filepath=02.Zoning_problem%2FEnviornment_lattice_generation%2FVoxelization%20for%20the%20massing%20models.ipynb)

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Voxelised_Base.png" >}}

Voxelised Base

# Eucledian Distance based simulations
