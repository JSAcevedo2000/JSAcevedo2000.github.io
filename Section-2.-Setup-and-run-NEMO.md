
## This section covers how to setup and run a NEMO tide and surge model in a docker container

**2.1.** We first have to set up a project space (called Belize_workshop) and obtain the necessary files:
     
     echo $HOME
     cd $HOME
     git clone https://github.com/NOC-MSM/Belize_workshop.git


**2.2.** We need to create a compatible docker environment. It has to match the environment in which the executables were built (~424Mb)::

     docker pull debian:jessie
     docker pull jelt/nemocompile:firsttry
     docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i jelt/nemocompile:firsttry /bin/bash



**2.3.** To run NEMO we need two executables: ``nemo.exe`` (the hydrodynamic model) and ``xios_server.exe`` (to handle input and output). These can either be downloaded into a controlled and compatible docker environment or built from scratch (see build NEMO instructions).

Copy the compiled executables to the run directory::

     cd /Belize_workshop/RUN_NEMO/EXP_demo
     
     wget ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/nemo_executables/nemo.exe
     wget ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/nemo_executables/xios_server.exe


**2.4.** Get Domain And Forcing Files or make sure you have them already
To run NEMO we need a number of essential files.
These files can all be downloaded into the target "EXP"eriment directory

Files required in the EXP directory::

	bdydta - directory of boundary forcing
	coordinates.bdy.nc - file specifying location of boundaries
	domain_cfg.nc - file describing the configuration domain / grid
	initcd_vosaline.nc - 3D initial condtions for salinity
	initcd_votemper.nc - 3D initial conditions for temperature
	metdta - directory of meteorological forcing
	runoff.nc - file containing river runoff data.

**ESTOS ARCHIVOS ESTAN EN ESTA LIGA DE DROPBOX (~500MB!!!!)
<https://www.dropbox.com/sh/8vlcoe1t4ne8zyd/AAClhLZ-rsGzNvewc1vquS4ua?dl=0>

---

If you don't have them already you can copy all the preprepared necessary files from an FTP site::

	cd /Belize_workshop/RUN_NEMO/EXP_demo

	wget -nH --cut-dirs=4 --no-parent --recursive ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/EXP_demo/


**2.5.** Run the model! 

Make sure exectuatables are executable::

	chmod a+rx nemo.exe
	chmod a+rx xios_server.exe

Submit your run (e.g. on a quad-core machine)::

	cd /Belize_workshop/RUN_NEMO/EXP_demo
	mpirun -n 3 ./nemo.exe : -n 1 ./xios_server.exe



### *If you encounter issues executing point 2.3.
You may need to add the user to the docker group::

$ sudo usermod -aG docker $USER
You will need to log out and then back in.
##
