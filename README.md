# TES-Analysis-Program
This repo contains a program written in python 3.7 for automatically analyzing TES data output in both a single setup and in a FDM setup. This software is the next generation from the software written by [Callum Blair](https://github.com/cgfb94/sensor-analysis) and contains a neural network written by [Arnold Dongelmans](https://github.com/AwesomeArnold/Neuralnetwork). The program itself contains a few examples that show the basics and how to access values and parameters.

# Downloading the Software
The program is contained in the TES_Analysis_Program.ipynb. This file can be downloaded and opened with jupyter notebook or similar notebook interpreters. 
A list of the library dependencies used for testing can be found in the troubleshooting directory. Using jupyter lab or any extension that allows for codefolding is recommended, as each individual class is rather large. 

# Program Walkthrough
The basic structure is as follows: All IV objects are stored within IV_series. Each IV object holds one dataset read out by one of the three read_data methods. 
There are 2 IV objects, `IV_single` and `IV_double`. The first class is able to analyze single sided datasets from the FDM setup, while the second one is able to analyze double sided datasets from a single TES detector, connected to a current source. Both these classes have options to calculate and plot certain values of their datasets. These operations can be done for all datasets by looping over the `data_single` or `data_double` list found in the `IV_series` class. 

## Importing Data
A directory (double sided data) or a list of filenames (single sided data) can be read out by the IV_series class.  

For the *double sided data*, all .qdp and .xlsx files will be read out in the given directory. The data is assumed to be in the order: I_bias, V_fb, T_BB, T_bath, Power. The final three columns are not necessary for analysis, but are necessary for calculating the final thermal conductance and critical temperature. 

For the *single sided data*, all filenames present in the filelist (conventionally .lis, can be any text file extension) will be read out. All FDM datasets are in .dat format, starting off with constants and with the data being present at the bottom of the file. 
Note that the path is set to the location of the filelist, and hence any files located in a directory above it must be accessed with ../file_name.dat. Alongside the path to the file, the Pixel, bath and BB values must be set in the filelist when they are necessary in the analysis. If not, they are set to zero.  

## Calculating Parameters
There are 2 ways of obtaining certain values. Firstly, the easiest way, is to use `IV_object.calc_all()`. This option calculates all values in the right order. Secondly, the functions can be called separately from each other. Do note that some functions require certain values that might not be present in the dataset, which are calculated somewhere else. 

## Multi-Set Graphs
The `IV_series` class also has several methods to plot calculated information from multiple datasets together. This is usually done by looping over all the datasets in either `data_double` or `data_single`, calculating all parameters and then plotting certain parameters from these calculated values for each dataset.  
