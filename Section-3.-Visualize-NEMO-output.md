NEMO outputs are **netCDF files** 
(<https://www.unidata.ucar.edu/software/netcdf/docs/>).

They can be visualized using different software i.e. **ncview**, **IDV** (<https://www.unidata.ucar.edu/software/netcdf/docs/>) or data analysis tools **R**, **MATLAB**, **IDL**, **PYTHON**.

To use the PYTHON script for plotting NEMO diagnostics, first build
the python environment, or check out the built executables from DockerHub. 

*At present (20 Sept) the python environment is about 3Gb...*


Take a clone of the workshop repository if you have not already, putting it
 somewhere like
``$HOME``::
     cd $HOME
     git clone https://github.com/NOC-MSM/Belize_workshop.git

###  Build PYTHON3 environment

Using a Docker instance install miniconda3 and then python modules for PARCELS
as follows::

     cd $HOME/Belize_workshop/PYTHON_TOOLS
     docker build -t blz_python .


Ensure all your data files are in this directory::

     cp <STUFF> $HOME/Belize_workshop/PYTHON_TOOLS/.

Run docker instance::

     docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i blz_python /bin/bash

     cd /Belize_workshop/PYTHON_TOOLS


### Checkout built executables

If the above is not very interesting and you want to get on with running python,
you can download an image of the above (~3Gb)::

     docker pull continuumio/miniconda3
     docker pull jelt/blz_python:firsttry

     docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i jelt/blz_python:firsttry /bin/bash
     cd /Belize_workshop/PYTHON_TOOLS
