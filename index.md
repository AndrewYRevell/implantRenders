---
layout: default
---

Made by Andy Revell (MD/PhD student at Penn)    ![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)


# Implant Links

**Click to view implant:**


| Subjects                                        |                                                 |                                                 |
| :---------------------------------------------  | :---------------------------------------------  | :---------------------------------------------  |
| [sub-RID0278](./renders/sub-RID0278/index.html) | [sub-RID0365](./renders/sub-RID0365/index.html) | [sub-RID0572](./renders/sub-RID0572/index.html) | 
| [sub-RID0583](./renders/sub-RID0583/index.html) | [sub-RID0595](./renders/sub-RID0595/index.html) | [sub-RID0596](./renders/sub-RID0596/index.html) | 
| [sub-RID0536](./renders/sub-RID0536/index.html) | [sub-RID0520](./renders/sub-RID0520/index.html) | [sub-RID0508](./renders/sub-RID0508/index.html) | 
| in progress                                     |                                                 |                                                 | 
| [sub-RID0502](./renders/sub-RID0502/index.html) | [sub-RID0490](./renders/sub-RID0520/index.html) | [sub-RID0454](./renders/sub-RID0508/index.html) | 

# About

These renders show implantations of epilepsy patients. Implantations were done for clinical purposes and to capture seizure activity. Click on the subject links in the table above to view the renders. You can adjust your view using your mouse and control settings (see below image). Click on "Channels" to see the channel label names. Spheres represent implanted electrode channels. The center of each sphere corresponds to the coordinate of each channel. Each spehere is arbitrarily 2.2 mm in radius. The coordinates of each channel is localized to specific brain tissue: gray matter (GM), white matter (WM), cerebrospinal fluid (CSF), or outside the brain area. 

Colored spheres correspond to these areas:

<span style="color:red">RED</span>: GM

<span style="color:blue">BLUE</span>: WM

<span style="color:purple">PURPLE</span>: CSF

WHITE: OUTSIDE (or not localized to any area)
 

![aboutImage](./pics/about.png)





#### Note on channel tissue localization:
The tissue type corresponding to each channel is determined by the SINGLE voxel the channel coordinate is in, and thus subject to errors.

Example: a specific voxel is determined to be GM through the FIRST and FAST FSL algorithms (see figure below). The channel is localized to that voxel. However, all surrounding voxels happen to be WM. It could be assumed then that the tissue type of that particular channel was determined to be wrong in this case - because all surrounding voxels of that channel are WM. 

The FIRST and FAST algorithms have a smoothing factor to mitigate this issue to some extent. Please take this into consideration when relying on the specifc tissue type of each channel when interpreting these localizations. See this image below for an overview of the localization procedure: 

![aboutImage](./pics/localization_v01.png)

Figure legend: Electrode localization and Tissue Segmentation. Each channel is localized to a specific tissue type shown by the figure above. (1) A CT is acquired of the implantation. (2) The coordinates of each channel is determined through our clinical localization pipeline, and registered to an implant image (3) and a preimplant image (4). Using the preimplant image, tissue type is determined using FSL's FIRST and FAST algorithms. Output of the cortical segmentation (FAST) is shown in (5) and output of the subcortical segmentation (FIRST) is shown in (6). These images are combined (7). The electrode coordinates are determined in preimplant space using FSL's linear registration (not non-linear - the figure is wrong here and will be updated). The exact coordinate of the electrode channel is matched to a voxel in the tissue segmentation combined image (7) and thus the type of tissue the channel is sampling from is determined. WARNING: This method does not consider surrounding voxels, and thus a channel may be erroneously determined to be sampling from the wrong tissue in rare cases.


# Metadata


| Subjects    | Implant        |  Sampling  |                                
| :---------- | :---------- | :--------- | 
| sub-RID0278 | SEEG        | bilateral  |
| sub-RID0365 | SEEG        | bilateral  |
| sub-RID0508 | SEEG        | left       |
| sub-RID0520 | SEEG + ECoG | left       |                                  
| sub-RID0536 | SEEG        | bilateral  |
| sub-RID0572 | SEEG        | right      |
| sub-RID0583 | SEEG        | left       | 
| sub-RID0595 | SEEG        | left       |
| sub-RID0596 | SEEG        | left       |


SEEG: Stereoelectroencephalography ("toothpicks")

ECoG: Electrocorticography ("grids and strips")







# Methods






### Visual

![visualMethodsImage](./pics/visualMethods.png)






### Bullet Point Methods

See [revellLab GitHub repository electrodeLocalization.py](https://github.com/andyrevell/revellLab/blob/main/packages/imaging/electrodeLocalization/electrodeLocalization.py) for example pipeline

1. Creation of brain 3D model
	- Data needed:
		- Pre-implant T1 image. 
		- Preferably at 3T
		- Preferably using our high resolution 3T research protocol (not all patients acquire this image)
	- Software needed:
		- Freesurfer
		- Blender 3.9
		- Python 3.7+
		- Script blender_compress_mesh.py from [revellLab GitHub repository](https://github.com/andyrevell/revellLab)
	- Step 1: Cortical surface reconstruction of brain 
		- Software: Freesurfer
		- Command: recon-all -subjid ### -all -time -log logfile -nuintensitycor-3T -sd ### -parallel -threads 12
		- Takes about 1.5-2hrs for Andy's computer (AMD Ryzen 9 3900X 12-Core Processor, 64 GB RAM, Titan RTX GPU)
	- Step 2: Make 3D model
		- Convert lh.pial and rh.pial to scanner T1 space
			- Freesurfer command: mris_convert --to-scanner lh.pial lh.pial
		- Combine lh.pial and rh.pial AND convert to .stl 3D model file
			- reesurfer command: mris_convert --combinesurfs rh.pial lh.pial combined.stl
		- Convert to .stl to .glb file (To render on webpage using three.js)
			- Software: Blender 3.9
			- Use python script blender_compress_mesh.py from [revellLab GitHub repository](https://github.com/andyrevell/revellLab/blob/main/packages/imaging/electrodeLocalization/blender_compress_mesh.py)
			- Command: blender --background --factory-startup --addons io_scene_gltf2 --python blender_compress_mesh.py -- -i combined.stl -o brain.glb
			
2. Get implantation coordinates
	- Data needed:
		- Pre-implant T1 image (from above)
		- Coordinates in the pre-implant T1 space above
			- If coordinates in a different space, need the corresponding T1 image and register the pre-implant T1 image above
		- Optional: output of [atlas localization pipeline](https://github.com/andyrevell/revellLab/blob/main/packages/atlasLocalization/atlasLocalization.py) to get tissue localization information of implant channels
	- Software needed:
		- FSL
		- Python 3.7+
	- Step 1: Register the pre-implant T1 image to the T1 image the coordinate file is in - skip if they are the same
		- Brain extract the images using FSL bet
		- Linear registration of the two images using FSL flirt
		- Apply the returned tranformation matrix from flirt to the coordinate file
			- FSL command: img2imgcoord -src ### -dest ### -xfm ### -mm ### > ###
			- See FSL's documentation of img2imgcoord for specific data sctructures files must be in
	- Step 2: Save coordinates in same location as the brain.glb file, name it electrodes.txt
		- electrodes.txt format
			- each row contains channel information. Column 1: Channel name; Column 2: x coordinate; Column 3: y coordinate; Column 4: z coordinate
			- Separation is a single space between columns (not comma or tab separated)
3. Get necessary files in single directory:
	- See [example](https://github.com/andyrevell/implantRenders/tree/main/renders/sub-RID0278) 
	- File names:
		- brain.glb
		- electrodes.txt
		- index.html [Get here]( https://github.com/andyrevell/revellLab/blob/main/tools/threejs/index.html)  
	- These three files are all you need, and the html file should work provided you name the .glb and .txt files accordingly
	- To run on local computer, follow [these directions](https://threejs.org/docs/#manual/en/introduction/How-to-run-things-locally) 
		- I installed npm: npm install http-server -g (I forget if you need this to run the python -m http.server below)
		- python -m http.server
		- Type this into browser (I used Chrome, Firefox, and Microsoft Edge): http://localhost:8000/
		- The reason why you need the above is because web browser restrict loading of the 3D .glb files locally for security reasons.
				
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
