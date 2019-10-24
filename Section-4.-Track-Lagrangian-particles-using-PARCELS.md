## PARCELS: Probably A Really Computationally Efficient Lagrangian Simulator <http://oceanparcels.org/>
"Is a set of Python classes and methods to create customisable particle tracking simulations using output from Ocean Circulation models. Parcels can be used to track passive and active particulates such as water, plankton, plastic and fish." 


## 4.1 Install PARCELS

**A)** If you have installed PARCELS before hand following the instructions on the webpage, you just need to start the *Anaconda Powershell prompt* and activate the python environment::
     
     source $HOME/miniconda3/bin/activate py3_parcels  # Linux / macOS
     activate py3_parcels                              # Windows


**B)** Otherwise we can modify the Docker container used to compile NEMO to work with PARCELS:
 
Go to: <https://docs.conda.io/en/latest/miniconda.html>

Download Linux python 3.7 64 bit miniconda install file. Save it into the *Belize_workshop* folder.

On the PowerShell terminal with Docker running open the NEMO container::


     docker pull debian:jessie
     docker pull jelt/nemocompile:firsttry
     docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i jelt/nemocompile:firsttry /bin/bash

Install Miniconda:

     bash Miniconda3-latest-Linux-x86_64.sh

Activate conda::

     eval "$(/root/miniconda3/bin/conda shell.bash hook)"

Update conda install::

     conda update conda

Install PARCELS::

     conda create -n py3_parcels -c conda-forge python=3 parcels jupyter cartopy ffmpeg



## 4.2 Run PARCELS
After completing **A)** or **B)** you can run PARCELS:

1) Activate the python environment for PARCELS

     conda activate py3_parcels

2) Run!   

     cd $HOME/Belize_workshop/PYTHON_TOOLS/PARCELS_DEMO
     python tinyBelize_Parcels.py

