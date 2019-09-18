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

Met data::

 metdta/*

These files can all be downloaded into a clean "EXP"eriment directory

---

Files required in the EXP00 directory::

	drwxr-xr-x   3 jeff  staff       96 18 Sep 12:59 bdydta
	-rw-r--r--   1 jeff  staff    37065 30 Jul 16:03 coordinates.bdy.nc
	-rw-r--r--   1 jeff  staff  4943472 26 Jul 16:28 domain_cfg.nc
	-rw-r--r--   1 jeff  staff  1029193 26 Jul 15:09 initcd_vosaline.nc
	-rw-r--r--   1 jeff  staff  1029193 26 Jul 15:09 initcd_votemper.nc
	drwxr-xr-x  17 jeff  staff      544 16 Sep 09:24 metdta
	-rw-r--r--   1 jeff  staff   211312 26 Jul 15:09 runoff.nc

---

Submit::

	cd /SRC/NEMOGCM/CONFIG/BELTOY/EXP
	mpirun -n 4 ./opa
