# Effects of The Panama Canal

This modeling project is an example to demonstrate the approximate scope, files, and organization of a class project for CS 185C.

## Project Description
In this project, I will be investigating the effects of the panama canal on both water salinity and average velocity in the areas around it specifically assuming that it is just a canal and not the more blocked multi layer system it is in reality. (Considering changing the project to see what happens if I flip all land on the planet 90 degrees similar to what is described in this video [https://www.youtube.com/watch?v=WH4g1ptJ-70] but am still uncertain). In Particular, I will be investigating the following science question:

*How would the panama canal affect the ocean salinity and current velocity should it be turned into a true canal?*

In order to investigate this question, I will construct a small and high resolution model right around the panama canal and some of its surrounding waters and run my model simulation for 2 years with 2 seperate setups: a run where the panama canal is treated as a through straigh and one where it is blocked off (not allowing water to diretly flow through the canal as in the real world. I will be running my experiment from 2008 to 2010. I anticipate some extra salinity on the pacific ocean side of the canal as the atlantic ocean is more saline than the pacific and the bay in that area is at higher elevation likely leading to flow going from the atlantic to the pacific.

For the initial conditions of the model I will import the ECCO version 5 model starting from january 2008. I will also be constructing a boundary for the model using gebco. In order to analyze the results I will track the changes in, velocity, salinity, and temparatue over time throughout the model, and use tools like matplotlib and moviepy in order to visualize the changes in the ocean over time, and compare them to one another.


## Reproducing Model Results

*Note for CS185C: The following section outlines possible steps that may be included in your README for reproducibility. When designing your own steps, be sure to consider which of the steps below pertain to your model and update/modify accordingly.*

The following steps outline how to construct the model files, configure and run the model, and assess the model results.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:
- Model Grid (notebooks/Creating the Model Grid.ipynb)
- Bathymetry (notebooks/Creating the Bathymetry.ipynb)
- Initial Conditions (notebooks/Creating the Initial Conditions.ipynb)
- External Forcing Conditions (notebooks/Creating the External Forcing Conditions.ipynb)
- Boundary Conditions (notebooks/Creating the Boundary Conditions.ipynb)
The model files should be placed into the  `input` directory.

### Step 2: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.
```
mkdir MITgcm/configurations/ca_upwelling
```
Then, use the `scp` command to send the `code`, `input`, and `namelist` directories to your configuration directory. 

### Step 3: Compile the model
Once all of the files are on the computing cluster, the model can be compiled. Make a `build` directory in the configuration directory and run the following lines:
```
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 4.1: Run the model with wind
After the compilation is complete, run the model with the wind. Move to the run directory, link everything from `input` and `code`, and the submit the job script:
```
sbatch cs185c.slm
```

### Step 4.2: Run the model without wind
Next, run the model without wind to complete the experiment. Again, link everything from `input` and `code` to a directory called `run_no_wind`. Then, edit the `data.exf` file to point to the modified wind files (see the Creating the External Forcing Conditions.ipynb notebook for details). Then, submit the job script again to rerun the model.

### Step 5: Analyze the Results
There are two notebooks provided for analysis:
1. Analyzing Model Results

   This notebook is provided to have a quick look at spatial and temporal variations in the temperature field in the model with wind. It also generates the visualization provided in the figures directory.
   
2. Answering the Science Question
   
   This notebooks provided some analysis plot to address the science question posed above.
