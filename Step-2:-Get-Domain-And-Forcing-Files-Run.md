To run NEMO we need a number of essential files.
These files can all be downloaded into the target "EXP"eriment directory

Files required in the EXP directory::

	drwxr-xr-x   3 jeff  staff       96 18 Sep 12:59 bdydta
	-rw-r--r--   1 jeff  staff    37065 30 Jul 16:03 coordinates.bdy.nc
	-rw-r--r--   1 jeff  staff  4943472 26 Jul 16:28 domain_cfg.nc
	-rw-r--r--   1 jeff  staff  1029193 26 Jul 15:09 initcd_vosaline.nc
	-rw-r--r--   1 jeff  staff  1029193 26 Jul 15:09 initcd_votemper.nc
	drwxr-xr-x  17 jeff  staff      544 16 Sep 09:24 metdta
	-rw-r--r--   1 jeff  staff   211312 26 Jul 15:09 runoff.nc

---

Something funny with the tides keys:  ``key_FES14_tides key_diaharm_fast`` -
cut them out and rebuilt!


Then copy in all the domain and forcing files::

	rsync -uvtr /Users/jeff/Desktop/temp/ /Users/jeff/Belize_workshop/RUN_NEMO/EXP_demo


Submit::

	cd /Belize_workshop/RUN_NEMO/EXP_demo
	mpirun -n 4 ./opa


This blows up after about 5 timesteps.
