If you have macOS or 64-bit Windows 10 Pro, Enterprise, and Education you will be able to install Docker following the instructions here <https://runnable.com/docker/getting-started/>

If you have an older Windows operating system you can try using Docker Toolbox instead: <https://docs.docker.com/toolbox/toolbox_install_windows/> you will get the executable from here: <https://github.com/docker/toolbox/releases>

Potential Fix for Docker toolbox issue when trying:
     docker run -v $HOME/Belize_workshop:/Belize_workshop -t -i jelt/nemocompile:firsttry /bin/bash
**_Error response from daemon: invalid mode: /Belize_workshop_**

     docker run -v /host_mnt/c/_**Users/gmaya**_:/Belize_workshop -t -i jelt/nemocompile:firsttry /bin/bash
