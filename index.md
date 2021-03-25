---
layout: default
---
**_No identifying patient information is present. The [18 HIPAA-designated](https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification/index.html) direct identifiers and other indirect identifiers are removed. Vague language is used to limit all attempts at identification (e.g. why surface reconstruction failed). This webpage is intended to navigate intracranial EEG implants in 3D space only._**
  
-------------------------------------
 
Made by Andrew Revell (Fifth-year MD/PhD student at Penn): 

[My GitHub](https://github.com/andyrevell)

<img src="./pics/londonPhone18.png" width="150">  

# Implant Links


**Click to view implant:**

|                                         |
| :-------------------------------------- | :-------------------------------------- | :-------------------------------------  | :-------------------------------------  | :-------------------------------------  | :-------------------------------------- | :-------------------------------------- | :-------------------------------------  | :-------------------------------------  | :-------------------------------------  |
| [31](./renders/sub-RID0031/index.html)  | 37                                      | 46                                      | 89                                      | [131](./renders/sub-RID0131/index.html) | [139](./renders/sub-RID0139/index.html) | [146](./renders/sub-RID0146/index.html) | [186](./renders/sub-RID0186/index.html) | [194](./renders/sub-RID0194/index.html) | [206](./renders/sub-RID0206/index.html) |
| [213](./renders/sub-RID0213/index.html) | [218](./renders/sub-RID0218/index.html) | [230](./renders/sub-RID0230/index.html) | [238](./renders/sub-RID0238/index.html) | 240                                     | 241                                     | 250                                     | 252                                     | 259                                     | 267                                     |
| 272                                     | 274                                     | [278](./renders/sub-RID0278/index.html) | [279](./renders/sub-RID0279/index.html) | 280                                     | 295                                     | 296                                     | 307                                     | [309](./renders/sub-RID0309/index.html) | 317                                     |      
| [320](./renders/sub-RID0320/index.html) | 322                                     | 325                                     | 328                                     | 329                                     | 330                                     | 332                                     | 334                                     | 337                                     | 338                                     |    
| [341](./renders/sub-RID0341/index.html) | 356                                     | 357                                     | [365](./renders/sub-RID0365/index.html) | 371                                     | [380](./renders/sub-RID0380/index.html) | 381                                     | 382                                     | 385                                     | 386                                     |  
| 392                                     | [394](./renders/sub-RID0394/index.html) | 405                                     | 412                                     | [420](./renders/sub-RID0420/index.html) | 424                                     | [440](./renders/sub-RID0440/index.html) | 442                                     | 452                                     | [454](./renders/sub-RID0454/index.html) | 
| [459](./renders/sub-RID0459/index.html) | [472](./renders/sub-RID0472/index.html)  | [475](./renders/sub-RID0475/index.html) | [476](./renders/sub-RID0476/index.html) | [490](./renders/sub-RID0490/index.html) | [502](./renders/sub-RID0502/index.html) | [508](./renders/sub-RID0508/index.html) | 517                                     | [520](./renders/sub-RID0520/index.html) | [522](./renders/sub-RID0522/index.html) |
| [529](./renders/sub-RID0529/index.html) | 530                                     | [536](./renders/sub-RID0536/index.html) | 560                                     | 562                                     | 566                                     | [572](./renders/sub-RID0572/index.html) | 582                                     | [583](./renders/sub-RID0583/index.html) | 588                                     |
| 589                                     | [595](./renders/sub-RID0595/index.html) | [596](./renders/sub-RID0596/index.html) | 646                                     | 647                                     | [648](./renders/sub-RID0648/index.html) | 649                                     | 650                                     | 651                                     | 652                                     |



- Notes:
	- 186: Surface reconstruction of pre-implant image failed in Freesurfer. Used alternative clinical T1 imaging. Non-linear registration of coordinates failed with alternative imaging. Therefore registered coordinates to the surface file are innacurate.
	- 194: Channel coordinates and surface reconstruction are correct. 
	- 476: Channel coordinates and surface reconstruction are correct. 


# About

These renders show implantations of epilepsy patients. Implantations were done for clinical purposes and to capture seizure activity. Click on the subject links in the table above to view the renders. You can adjust your view using your mouse and control settings (see below image). On mobile, toggle off "Brain wireframe" for quicker view adjustments. Click on "Channels" to see the channel label names. Spheres represent implanted electrode channels. The center of each sphere corresponds to the coordinate of each channel. Each spehere is arbitrarily 2.2 mm in radius. The coordinates of each channel is localized to specific brain tissue: gray matter (GM), white matter (WM), cerebrospinal fluid (CSF), or outside the brain area. 

Colored spheres correspond to these areas:

<span style="color:red">RED</span>: GM

<span style="color:blue">BLUE</span>: WM

<span style="color:purple">PURPLE</span>: CSF

WHITE: OUTSIDE (or not localized to any area)
 

![aboutImage](./pics/about.png)





#### Note on channel tissue localization:
The tissue type corresponding to each channel is determined by the SINGLE voxel the channel coordinate is in, and thus subject to errors.

Example: a specific voxel is determined to be GM through the FIRST and FAST FSL algorithms (see figure below). The channel is localized to that voxel. However, all surrounding voxels happen to be WM. It could be assumed then that the tissue type of that particular channel was determined to be wrong in this case - because all surrounding voxels of that channel are WM. Furthermore, tissue localization for ECoG (grids and strips) may not be necessarily correct. They can be assumed to be in CSF overlaid on GM cortical structures.

The FIRST and FAST algorithms have a smoothing factor to mitigate this issue to some extent. Please take this into consideration when relying on the specifc tissue type of each channel when interpreting these localizations. See this image below for an overview of the localization procedure: 

![aboutImage](./pics/localization_v01.png)

Figure legend: Electrode localization and Tissue Segmentation. Each channel is localized to a specific tissue type shown by the figure above. (1) A CT is acquired of the implantation. (2) The coordinates of each channel is determined through our clinical localization pipeline, and registered to an implant image (3) and a preimplant image (4). Using the preimplant image, tissue type is determined using FSL's FIRST and FAST algorithms. Output of the cortical segmentation (FAST) is shown in (5) and output of the subcortical segmentation (FIRST) is shown in (6). These images are combined (7). The electrode coordinates are determined in preimplant space using FSL's linear registration (not non-linear - the figure is wrong here and will be updated). The exact coordinate of the electrode channel is matched to a voxel in the tissue segmentation combined image (7) and thus the type of tissue the channel is sampling from is determined. WARNING: This method does not consider surrounding voxels, and thus a channel may be erroneously determined to be sampling from the wrong tissue in rare cases.


# Metadata


| Subject | Implant     |  Sampling  | T1 scan used for surface  |                                
| :------ | :---------- | :--------- | :------------------------ |
| 31      | SEEG        | bilateral  | research 3T protocol      |
| 131     | SEEG        | left       | clinical pre-op 3T scan   |
| 139     | SEEG        | bilateral  | research 3T protocol      |
| 146     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 186     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 194     | SEEG        | bilateral  | research 3T protocol      |
| 206     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 213     | ECoG        | bilateral  | research 3T protocol      |
| 218     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 230     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 238     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 278     | SEEG        | bilateral  | research 3T protocol      |
| 279     | SEEG        | bilateral  | clinical pre-op 3T scan   |
| 309     | SEEG        | bilateral  | research 3T protocol      |
| 320     | SEEG        | bilateral  | research 3T protocol      |
| 341     | SEEG        | bilateral  | research 3T protocol      |
| 365     | SEEG        | bilateral  | research 3T protocol      |
| 380     | SEEG        | bilateral  | research 3T protocol      |
| 394     | SEEG        | bilateral  | research 3T protocol      |
| 420     | SEEG        | bilateral  | research 3T protocol      |
| 440     | SEEG        | bilateral  | research 3T protocol      |
| 454     | SEEG        | bilateral  | research 3T protocol      |
| 459     | SEEG        | left       | research 3T protocol      |
| 475     |         |   | clinical pre-op 3T scan      |
| 476     | SEEG        | bilateral  | research 3T protocol      |
| 490     | SEEG        | bilateral  | research 3T protocol      |
| 502     | SEEG        | bilateral  | research 3T protocol      |
| 508     | SEEG        | left       | research 3T protocol      |
| 520     | SEEG + ECoG | left       | research 3T protocol      | 
| 522     | SEEG        | right      | research 3T protocol      |
| 529     | SEEG        | right      | research 3T protocol      |                                   
| 536     | SEEG        | bilateral  | research 3T protocol      |
| 572     | SEEG        | right      | research 3T protocol      |
| 583     | SEEG        | left       | research 3T protocol      | 
| 595     | SEEG        | left       | research 3T protocol      |
| 596     | SEEG        | left       | research 3T protocol      |
| 648     | SEEG        | left       | research 3T protocol      |





SEEG: Stereoelectroencephalography ("toothpicks")

ECoG: Electrocorticography ("grids and strips")







# Methods






### Visual

![visualMethodsImage](./pics/visualMethods.png)






### Bullet Point Methods

See [revellLab GitHub repository electrodeLocalization.py](https://github.com/andyrevell/revellLab/blob/main/packages/imaging/electrodeLocalization/electrodeLocalization.py) for example pipeline

1. **Step 1: Creation of brain 3D model**
	- Data needed:
		- Pre-implant T1 image. 
		- Preferably at 3T
		- Preferably using our high resolution 3T research protocol (not all patients acquire this image)
	- Software needed:
		- Freesurfer
		- Blender 3.9
		- Python 3.7+
		- Script blender_compress_mesh.py from [revellLab GitHub repository](https://github.com/andyrevell/revellLab)
	- Step 1.1: Cortical surface reconstruction of brain 
		- Software: Freesurfer
		- Command: recon-all -subjid ### -all -time -log logfile -nuintensitycor-3T -sd ### -parallel -threads 12
		- Takes about 1.5-2hrs for Andy's computer (AMD Ryzen 9 3900X 12-Core Processor, 64 GB RAM, Titan RTX GPU)
	- Step 1.2: Make 3D model
		- Convert lh.pial and rh.pial to scanner T1 space
			- Freesurfer command: mris_convert --to-scanner lh.pial lh.pial
		- Combine lh.pial and rh.pial AND convert to .stl 3D model file
			- reesurfer command: mris_convert --combinesurfs rh.pial lh.pial combined.stl
		- Convert to .stl to .glb file (To render on webpage using three.js)
			- Software: Blender 3.9
			- Use python script blender_compress_mesh.py from [revellLab GitHub repository](https://github.com/andyrevell/revellLab/blob/main/packages/imaging/electrodeLocalization/blender_compress_mesh.py)
			- Command: blender --background --factory-startup --addons io_scene_gltf2 --python blender_compress_mesh.py -- -i combined.stl -o brain.glb
			
2. **Step 2: Get implantation coordinates**
	- Data needed:
		- Pre-implant T1 image (from above)
		- Coordinates in the pre-implant T1 space above
			- If coordinates in a different space, need the corresponding T1 image and register the pre-implant T1 image above
		- Optional: output of [atlas localization pipeline](https://github.com/andyrevell/revellLab/blob/main/packages/atlasLocalization/atlasLocalization.py) to get tissue localization information of implant channels
	- Software needed:
		- FSL
		- Python 3.7+
	- Step 2.1: Register the pre-implant T1 image to the T1 image the coordinate file is in - skip if they are the same
		- Brain extract the images using FSL bet
		- Linear registration of the two images using FSL flirt
		- Apply the returned tranformation matrix from flirt to the coordinate file
			- FSL command: img2imgcoord -src ### -dest ### -xfm ### -mm ### > ###
			- See FSL's documentation of img2imgcoord for specific data sctructures files must be in
	- Step 2.2: Save coordinates in same location as the brain.glb file, name it electrodes.txt
		- electrodes.txt format
			- each row contains channel information. Column 1: Channel name; Column 2: x coordinate; Column 3: y coordinate; Column 4: z coordinate
			- Separation is a single space between columns (not comma or tab separated)
3. **Step 3: Get necessary files in single directory:**
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
				
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
