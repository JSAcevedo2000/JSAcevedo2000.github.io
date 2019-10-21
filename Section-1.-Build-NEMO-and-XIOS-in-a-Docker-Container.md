## Here we can either build our own nemo executables or we can checkout a pre-build
version. However we first have to set up a project space (called ``Belize_workshop``) and obtain necessary files::

	cd $HOME
	git clone https://github.com/NOC-MSM/Belize_workshop.git


To run NEMO we need two executables: ``nemo.exe`` (the hydrodynamic model) and ``xios_server.exe`` (to handle input and output). These can either be downloaded into a controlled and compatible docker environment or built from scratch.


---


Obtain built executables
========================

First create a compatible docker environment that matches the environment in which the executables were built (~424Mb)::

	docker pull debian:jessie
	docker pull jelt/nemocompile:firsttry
	docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i jelt/nemocompile:firsttry /bin/bash


You may need to add the user to the docker group::

	$ sudo usermod -aG docker $USER

You will need to log out and then back in.

Then copy in the compiled executables to the run directory::

	cd /Belize_workshop/RUN_NEMO/EXP_demo

	wget ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/nemo_executables/nemo.exe
	wget ftp://livftp01.nerc-liv.ac.uk/noc/Belize_workshop/data/nemo_executables/xios_server.exe





Build NEMO executables
======================

Follow the steps below as there is some differences to Pierre's method::

	cd $HOME/Belize_workshop/BUILD_NEMO

Checkout NEMO code and XIOS code into directories at same level as NEMO-Docker::

	svn co http://forge.ipsl.jussieu.fr/nemo/svn/trunk/NEMOGCM@8395 NEMOGCM
	svn co -r1242 http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0_r1242
	ln -s xios-2.0_r1242/ XIOS2

Copy the arch files that came from Pierre's github into the NEMO tree::

	cp arch_NEMOGCM/arch* NEMOGCM/ARCH; cp arch_XIOS/arch* XIOS2/arch



The docker image can now be built::

	cd Docker
	docker build -t nemocompile .

You may need to add the user to the docker group::

	$ sudo usermod -aG docker $USER

You will need to log out and then back in.

The image can now be run, the path to SRC needs to be absolute, so switch
``/Users/jeff`` to the output of "echo $HOME"::

	docker run -v /Users/jeff/Belize_workshop:/Belize_workshop -t -i nemocompile /bin/bash

This should result in the container running and the terminal will move to the container e.g. (root@"container id"#) XIOS can now be compiled::

	cd /Belize_workshop/BUILD_NEMO/XIOS2
	./make_xios --dev --netcdf_lib netcdf4_seq --arch DEBIAN

This should successfully build and result in an executable in the XIOS
 directories, ``xios_server.exe``, which will need to go into the EXPeriment
 directory at run time. *(It took 30 mins on my Mac)*.

Some environmental variables need to be defined (this can't be
  done until inside the container)::

	export CONFIG=BLZ
	export WDIR=/Belize_workshop
	export CDIR=$WDIR/BUILD_NEMO/NEMOGCM/CONFIG
	export EXP=$WDIR/RUN_NEMO/EXP_demo

NEMO can now be built. Create an empty configuration::

	cd $CDIR
	./makenemo -n $CONFIG -m DEBIAN clean

Answer yes to the first question (OPA_SRC), no to all the others.

Copy MY_SRC fortran modifications into directory::

	cp -r $WDIR/BUILD_NEMO/MY_SRC $CDIR/$CONFIG/.

Copy compiler flag options into directory::

	cp $WDIR/BUILD_NEMO/cpp_file.fcm $CDIR/$CONFIG/cpp_BLZ.fcm

Then build NEMO again::

	./makenemo -n $CONFIG -m DEBIAN

This should build a nemo.exe file. At this point you can abandon BUILD_TOOLS except for two executables that need to go into an EXPeriment directory::

	ln -s $WDIR/BUILD_NEMO/xios-2.0_r1242/bin/xios_server.exe $EXP/xios_server.exe
	ln -s $CDIR/$CONFIG/BLD/bin/nemo.exe $EXP/nemo.exe

	---

	You should now be ready to run NEMO.
