# `mdanalysis` – Post processing of MD 

## Overview

`mdanalysis.py` is a Python script that provides a set of tools for processing MD trajectory files generated by [**SPARC**](https://github.com/SPARC-X/SPARC/) and calculating various quantities such as total internal energy, total pressure, self-diffusion coefficient, inter-diffusion coefficient, shear viscosity, and pair-correlation funcions.

## Requirements

To use `mdanalysis.py`, you need the following:

- Python 3.6 or later
- Numpy


## Usage
```shell
$ python mdanalysis.py carbon.mdanalysis.inpt
```
To use the `mdanalysis.py` one needs an input file `carbon.mdanalysis.inpt` which contains the following variables. 
 * `SYSTEM_NAME:` - Name of the system. This will determine the names of the file (e.g. C2.out, C2.aimd, C2.out_01 etc)
 * `N_FOLDERS:` - Number of folders used to run the simulation (Each folder will be considered a MD trajectory with an indepedent starting point)
 * `FOLDER_PATH_SIMULATIONS:` - Location of the folders
 * `N_SIMULATIONS_FOLDER:` -Number of simulation run within each folder (If it has 3 simulations, C2.out, C2.out_01, C2.out_02 files are expected.)
 * `N_EQUIL:` - Number of MD steps for equilibriation
 * `PCF_FLAG:` - Flag to do a pair correlation function calculation
 * `RANGE_PCF:` - Maximum radial distance to be  considered 
 * `SIZE_HIST_PCF:` - Total number of spherical shells to be considered
 * `SELF_DIFFUSION_FLAG:` - Flag to do self-diffusion coefficient calculation using integration of VACF
 * `BLOCK_LENGTH_SELF_DIFFUSION:` - Block lengths for self diffuison calculation (provide a block length for each elemental specie in the system)
 * `INTER_DIFFUSION_FLAG:` - Flag to do inter-diffusion coefficient calculation using integration of VACF
 * `BLOCK_LENGTH_INTER_DIFFUSION:` - Block length for inter diffuison calculation
 * `VISCOSITY_FLAG:` - Flag to do shear viscosity calculation using integration of VACF
 * `BLOCK_LENGTH_VISCOSITY:` - Block length for viscosity calculation
 * `INTERNAL_ENERGY_FLAG:` - Flag to get the mean and error bar of total internal energy (ha/atom)
 * `PRESSURE_FLAG:` - Flag to get the mean and error bar of total pressure (GPa)

An output file named `carbon.mdanalysis.out` will be written with all the values.
## Usage
 * The inter-diffusion coefficient has only been implemented for binary systems. 
 * The error bar has been calculated using the re-blocking method (https://web.ornl.gov/~kentpr/thesis/pkthnode31.html). The data for the standard deviation, block-size is also written in a text file. Please check these files to ensure that the standard deviations have reached close to limiting values
 * For diffusion coefficients and viscosity, velocity autocorrelation function (VACF) and stress autocorrelation function (SACF) has also been written in files `vacf.txt` and `sacf.txt`. Check these files to make sure that they have decayes to zero for the specified block length. 
 * The block length for diffusion coefficients and viscosity calculation needs to be tuned by the user such that the corresponding auto-correlation functions have decayed to zero.

## Example

Explore an example of how to use `mdanalysis` to calculate for a dummy carbon system in the `example/` directory.



