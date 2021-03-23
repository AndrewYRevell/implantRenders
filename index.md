---
layout: default
---

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png) Made by Andy Revell (MD/PhD student at Penn)


# Implant Links

**Click to view implant:**


| Subjects                                        |                                                 |                                                 |
| :---------------------------------------------  | :---------------------------------------------  | :---------------------------------------------  |
| [sub-RID0278](./renders/sub-RID0278/index.html) | [sub-RID0365](./renders/sub-RID0365/index.html) | [sub-RID0572](./renders/sub-RID0572/index.html) | 
| [sub-RID0583](./renders/sub-RID0583/index.html) | [sub-RID0595](./renders/sub-RID0595/index.html) | [sub-RID0596](./renders/sub-RID0596/index.html) | 


# About

To do: Full description of methods

1. Creation of brain 3D model
	- Use preimplantation pre-implant T1 image. 
		- Preferably at 3T
		- Preferably using our high resolution 3T research protocol (not all patient acquire)
	- Cortical surface reconstruction of brain 
		- Software: Freesurfer
		- Command: recon-all -subjid ### -all -time -log logfile -nuintensitycor-3T -sd ### -parallel -threads 12
		- Takes about 1.5-2hrs for Andy's computer (AMD Ryzen 9 3900X 12-Core Processor, 64 GB RAM, Titan RTX GPU)
	- Make 3D model
		- Convert lh.pial and rh.pial to scanner T1 space
			- Freesurfer command: mris_convert --to-scanner lh.pial lh.pial
		- Combine lh.pial and rh.pial AND convert to .stl 3D model file
			- reesurfer command: mris_convert --combinesurfs rh.pial lh.pial combined.stl
		- Convert to .stl to .glb file (To render on webpage using three.js)
			- Software: Blender 3.9
			- Use python script from [revellLab GitHub repository](https://github.com/andyrevell/revellLab)
				- /packages/imaging/electrodeLocalization/blender_compress_mesh.py
			- Command: blender --background --factory-startup --addons io_scene_gltf2 --python blender_compress_mesh.py -- -i combined.stl -o brain.glb
			
2. Get implantation coordinates
	
			
