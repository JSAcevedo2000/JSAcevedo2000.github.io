# # Build PARCELS environment

Using a Docker instance install miniconda3 and then python modules for PARCELS
as follows::

  cd /Belize_workshop/PARCELS_DEMO

  docker build -t parcels .


Ensure all your data files are in this directory.

  cp <STUFF> /Belize_workshop/PARCELS_DEMO/.

Run docker instance::

  docker run -v /Users/jeff/Belize_workshop/PARCELS_DEMO:/PARCELS_DEMO -t -i parcels /bin/bash


Then you can start python, and hopefully do things::

  python <filename>
