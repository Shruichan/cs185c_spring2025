# What would happen if we rotated the earth


## Project Description

In this project, I will be investigating the effects of a hypothetical 90-degree rotation of the Earth along its mantle in which the current equator becomes a meridian and the poles are relocated to what are now equatorial regions. This simulation is inspired by the thought experiment discussed in this video: [https://www.youtube.com/watch?v=WH4g1ptJ-70].

In particular, I will be investigating the following science question:

*How would a 90-degree rotation of the Earth affect global ocean salinity, temperature, and current velocity patterns?*

To investigate this question, I will generate a modified Earth topography by rotating a current bathymetry file and coarsening it for easier model running. Using this new orientation, I will configure a global ocean circulation model and run simulations under the new geography. Specifically, I plan to run the model into the future as I will be using the latest GEBCO dataset for the rotated bathymetry

In order to analyze the results I will track the changes in, velocity, salinity, and temparatue over time throughout the model, and use tools like matplotlib and moviepy in order to visualize the changes in the ocean over time, and compare them to one another.

This simulation will help explore how drastically the continents and earth land configuration affects life as we know it and will provide good insight as to what would happen ecologically as well should the earth magically get rotated.





## Reproducing Model Results

*Note for CS185C: The following section outlines possible steps that may be included in your README for reproducibility. When designing your own steps, be sure to consider which of the steps below pertain to your model and update/modify accordingly.*

The following steps outline how to construct the model files, configure and run the model, and assess the model results.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:
- Model Grid (notebooks/Creating the Model Grid.ipynb)
- Bathymetry (notebooks/Creating the Bathymetry.ipynb)
- Initial Conditions (notebooks/Creating the Initial Conditions.ipynb) namely S_IC and T_IC . bin make sure to replace lev_sss and lev_sst.bin in your input directoru
The model files should be placed into the  `input` directory.

### Step 2: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory.
Then navigate to the input direcectory of tutorial_global_oce_latlon in the verification folder. And replace the bathymetry file with the rotated one you generated and replace lev_sss and lev_sst .bin with the rotated initial condition files.

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


### Step 5: Analyze the Results
There are two notebooks provided for analysis:
1. Analyzing Model Results

   Currently there are no model results however we can make predictions as to what will happen.
   
2. Answering the Science Question
   
   This notebooks provided some analysis plot to address the science question posed above.
