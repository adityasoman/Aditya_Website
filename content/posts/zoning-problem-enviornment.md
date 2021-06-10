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

## QuitenessLattices

The Quiteness Lattice is a measure of the sound pressure recieved at each of the locations in the mass or the voxelated grid.The calculations related to the sound insulation are complicated and require a lot of data with respect to the material qualities of the building the sound pressure at the source of sound etc.The general equation for airborne sound insulation of a facade is given as:


The distance from the source of the sound to the room is critical in this calculation and there can be a 6Db reduction in the sound pressure level with doubling of the distance from the source.This relation can be easily calculated, and will provide a good estimate for decision making regarding the quietness of the voxel with respect to the source of sound.The code for calculating the same would be as follows:

```python
# Upload base voxel grid
# Upload Context meshes
# Upload Noise source locations

# Find the voxel Eucledian coordinates
# convert to lattice
init_lattice = envelope_lattice +1
availability_lattice_voxels = tg.to_lattice(init_lattice, init_lattice)
voxel_coordinates= availability_lattice_voxels.centroids
flattened_lattice = envelope_lattice.flatten()

# Find distances for Quiteness 
# The distance from each source of sound is calculated and the minimum distance from them is choosen

Eucledian_distance = sc.spatial.distance.cdist(Noise_sources,voxel_coordinates)
noise_from_each_source = Eucledian_distance.T
Average_quiteness_indexing= np.argmin(noise_from_each_source, axis=1)
Average_quiteness_values = []

for branch,index in zip(noise_from_each_source,Average_quiteness_indexing):
    Average_quiteness_values.append(branch[index])
  
Quiteeness_lattice_padded= np.array([num if boolean else 0 for boolean, num in zip(flattened_lattice, cycle(Average_quiteness_values))])

padded_array = np.array(Quiteeness_lattice_padded)

Quiteness_lattice_np = Quiteeness_lattice_padded.reshape(envelope_lattice.shape)

Quiteness_lattice =tg.to_lattice(Quiteness_lattice_np, Quiteness_lattice_np.shape)


```

{{< image src="https://raw.githubusercontent.com/adityasoman/Aditya_Website/main/content/Images/Voxelised_Base.png" >}}

## Closeness to the Facades Lattices

The facade closeness lattice determines the distance of the voxels in an lattice with respect to the outermost voxels in a specified direction. The code for calculating the same would be as follows:
