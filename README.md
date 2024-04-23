﻿# 3D-Cycle-conversion-and-reconstruction-Network
*******************************************************************************
## Requirements
Additional packages can be installed with "pip install -r requirements.txt"
*******************************************************************************
## Python scripts and their function

- organize_folder_structure.py: Organize the data in the folder structure (training,testing) for the network.

- check_loader_patches: Shows example of patches fed to the network during the training.

- options_folder/base_options.py: List of base_options used to train/test the network.  

- options_folder/train_options.py: List of specific options used to train the network.

- options_folder/test_options.py: List of options used to test the network.

- utils_folder: contains the Nifti_Dataset Dataloader and augmentation functions to read and augment the data.

- models_folder: the folder contains the scripts with the networks and the cycle-gan training architecture.

- train.py: Runs the training. (Set the base/train options first)

- test.py: It launches the inference on a single input image chosen by the user. (Set the base/train options first)
*******************************************************************************
## Usage
### Folders structure:

Use first "organize_folder_structure.py" to create organize the data.
Modify the input parameters to select the two folders: images and labels folders with the dataset.
(Example, I want to obtain SPECT from MRI brain images)


    .
	├── Data_folder                   
	|   ├── MRI_Brain               
	|   |   ├── image1.nii 
    |   |   ├── image2.nii 	
	|   |   └── image3.nii                     
	|   ├── SPECT_Brain                        
	|   |   ├── image1.nii 
    |   |   ├── image2.nii 	
	|   |   └── image3.nii  

Data structure after running it:

	.
	├── Data_folder                   
	|   ├── train              
	|   |   ├── images (MRI)            
	|   |   |   ├── 0.nii              
	|   |   |   └── 1.nii                     
	|   |   └── labels (SPECT)            
	|   |   |   ├── 0.nii             
	|   |   |   └── 1.nii
	|   ├── test              
	|   |   ├── images (MRI)           
	|   |   |   ├── 0.nii              
	|   |   |   └── 1.nii                     
	|   |   └── labels (SPECT)            
	|   |   |   ├── 0.nii             
	|   |   |   └── 1.nii
	
To make the training work it is necessary that the train images and labels have same matrix size and same origin/direction, because the program extracts image patches with the SimpleITK functions (or take the all image if you set the same size). 
*******************************************************************************
### Training:
- Modify the options to set the parameters and start the training/testing on the data. Read the descriptions for each parameter.
- Afterwards launch the train.py for training. Tensorboard is not available to monitor the training: you have to stop the training to test the checkpoints weights. You can continue the training
by loading them and setting the correspondent epoch.
*******************************************************************************
### Inference:
Launch "test.py" to test the network. Modify the parameters in the test_options parse section to select the path of image to infer and result. First you have to rename the weights "latest_net_GA" in:
"latest_net_G" to go from images (MRI) to labels (SPECT). Do the same with latest_net_GB to go in the opposite direction.

*******************************************************************************


