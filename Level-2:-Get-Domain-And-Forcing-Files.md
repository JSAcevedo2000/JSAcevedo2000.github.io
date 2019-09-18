To run NEMO we need a number of essential files.

DOMAIN::

	domain_cdf.nc
	coordinates.bdy.nc

INITIAL CONDITIONS::

  .nc

OBC (open boundary conditions)::

	.nc

TIDES (tidal forcing at the boundaries)::

	.nc

SBC (surface forcing)::

	.nc


Namelist files to control the simulation and output::

	namelist_cfg
	namelist_ref

	context_nemo.xml
	domain_def_nemo.xml
	field_def_nemo-lim.xml
	field_def_nemo-opa.xml
	file_def_nemo.xml
	iodef.xml

RIVERS::

	runoff.nc


These files can all be downloaded into a clean "EXP"eriment directory

Link in the nemo and xios executables::

	cd EXP
	ln -s /SRC/NEMOGCM/CONFIG/BELTOY/BLD/bin/nemo.exe opa
	ln -s /SRC/xios-2.0_r1080/bin/xios_server.exe xios_server.exe
