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

---



Copy all the preprepared necessary files from an FTP site::

	cd /Belize_workshop/RUN_NEMO/EXP_demo

	wget -nH --cut-dirs=4 --no-parent --recursive ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/EXP_demo/

Make sure exectuatables are executable::

	chmod a+rx nemo.exe
	chmod a+rx xios_server.exe

Submit::

	cd /Belize_workshop/RUN_NEMO/EXP_demo
	mpirun -n 4 ./nemo.exe : -n 1 ./xios_server.exe
