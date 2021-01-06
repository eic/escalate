Containers
==========

We use Docker as the default containerization technology. Singularity is also can be easily used utilizing docker images. 

The primary goal of the images is to provide an easy means for scientists to start running EIC software. There 4 main images:


* electronioncollider/eic-science
* electronioncollider/eic-mceg
* electronioncollider/escalate
* electronioncollider/escalate-gui

.. image:: https://gitlab.com/eic/containers/-/blob/master/docker-hierarhy.svg


Software version table ESCalate 1.1.0
-------------------------------------


(Changed packet versions and new packets are bold)

+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
|         Core tools        |            HENP           |           MCEG            |            EIC            |
+=============+=============+=============+=============+=============+=============+=============+=============+
| **Packet**  | **Version** | **Packet**  | **Version** | **Packet**  | **Version** | **Packet**  | **Version** |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| gcc         | 9.2.1       | hepmc       | 2.6.9       | LHAPDF6     | 6.2.3       | ejpm        | **0.3.21**  |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| CMake       | 3.17.0      | hepmc3      | 3.2.1       | pythia8     | 8.244       | eic-smear   |  1.0.4f1    |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| python      | 3.7.5       | vgm         | 4.5         | DIRE        | 2.004       | jana        | **2.0.3**   |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| eigen3      | 3.3.7       | genfit      | 2020.1      | Cernlib     | 2006-12-20  | ejana       | **1.2.3**   |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| clhep       | 2.3.2.2     | acts        | **0.22.01** | lhapdf5     | 5.9.1-6     | g4e         | **1.3.5**   |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| ROOT        | 6-20-04     | delphes     | 3.4.2       | PYTHIA6     | RAD-CORR    | **smear**   | **0.1.6**   |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+
| Geant4      | 10.6.1      | fastjet     | 3.3.3       |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+

[#] - See CHANGELOG.rst for other versions



`EIC software quick start tutorial <https://eic.gitlab.io/documents/quickstart/>`_

Installing Docker
-----------------

The Docker_ virtualization software is available for Linux, macOS, and Windows. Please follow the instructions to install, configure, and test Docker on your system: 

- **Linux**: `Docker Engine`_ (free in the Community Edition)
- **macOS**: `Docker Desktop`_ (free)
- **Windows**: `Docker Desktop`_ (free)

.. _Docker: https://hub.docker.com 
.. _Docker Desktop: https://www.docker.com/products/docker-desktop
.. _Docker Engine: https://hub.docker.com/search/?type=edition&offering=community


Obtaining the EIC Software image
--------------------------------

The EIC Software images are deployed using the electronioncollider swarm on Docker Hub. The latest versions can be obtained via: 

.. code-block:: bash

    docker pull electronioncollider/escalate:v1.1.0

This requires Docker to be running on the local system. 
Please see the `Troubleshoot`_ section if you receive the error message of ```no space left on device```. 


Running the EIC Software image
------------------------------

The EIC Software images provide an interactive environment which can be started via: 

.. code-block:: bash

   docker run -it --rm -p8888:8888 electronioncollider/escalate:v1.1.0


and can be accessed via the host system’s native web browser.

.. code-block:: bash

   http://127.0.0.1:8888/


This requires Docker to be running on the local system. The ```--rm``` flag is used to automatically clean up the container and remove the file system (and all modified and created files with it) when the container exits.  The flag is included for the sake of tutorials but not needed when working with the JupyterLab environment where retaining all data in the container (including all changes and modifications) might be preferred. By default (without ```--rm``` flag), a container’s file system persists even after the container exits. 


Troubleshoot
------------

If docker gives an error like this:
> Error starting userland proxy: listen tcp 0.0.0.0:8888: bind: address already in use.

It usually means, that the port 8888 is used by another application. 
To fix that try to change `-p 8888:8888` flag to `-p <something>:8888` 
e.g. `-p 9999:8888`. Put the same port in your browser:


.. code-block:: bash

   127.0.0.1:9999/lab


Occasionally, the error message of ``no space left on device`` has been reported when pulling large Docker images. In most cases, this can be prevented by removing all unused containers, images and more via ``docker system prune -a``. On macOS, it might be also required to increase the ``disk image size``. You find the option in the Docker Desktop application when selecting ``Preferences`` and ``Resources``. 



X11 - Working with GUI
----------------------

There are several ways of dealing with native GUI applications for 
escalate and escalate-gui images. E.g. showing standard root browser or Geant4 event viewer. 

1. SSH -X
2. X11 directly

What is the best option:



1. SSH -X
.........

eicuser password is eicuser

.. code-block:: bash

    docker run --rm -it -p127.0.0.1:2222:22 electronioncollider/escalate:latest runssh


connect with SSH:

.. code-block:: bash

    ssh -X eicuser@127.0.0.1 -p 2222



2. X11
......

The most convenient is using X11 directly. It require x11 client apps on Macs and Windows and may have some issues with user id's and permissions on Posix (max & linux). 
It might sound complex, but actiually it is simple and works most of the times. Still we don't use this way for the tutorials, but it is available in the documentation. 

**Requirements**: X11 cliens (windows and mac), additional docker flags (see of each OS)


You can use X11 natively (as natively as possible) with this docker image in your system:

Linux
^^^^^

To use graphics, make sure you are in an X11 session and run the following command: 

.. code-block:: bash

    docker run -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --rm -it --user $(id -u) -p8888:8888 electronioncollider/escalate


There might be issues with user id on systems like JLab farms. 

Windows
^^^^^^^

To enable graphics, you must have `VcXsrv <https://sourceforge.net/projects/vcxsrv/files/latest/download>`_ installed. 
Make sure VcXsrv is whitelisted in the Windows firewall when prompted. 

Start VcXsrv with 'allow from any origin' flag

.. code-block:: bash

    docker run --rm -it -p 8888:8888 -e LIBGL_ALWAIS_INDIRECT=1 -e DISPLAY=10.0.75.1:0  electronioncollider/escalate bash


OSX
^^^

To use graphics on OSX, make sure XQuarz is installed. 
After installing, open XQuartz, and go to XQuartz, Preferences, select the Security tab, and tick the box 
"Allow connections from network clients". Then exit XQuarz. 

Afterwards, open a terminal and run the following commands: 

.. code-block:: bash

    ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 

    echo $ip   # To make sure it was successfull
               # If nothing is displayed, replace en0 with en1 and so on
           
    xhost + $ip  # start XQuartz and whitelist your local IP address


This will start XQuartz and whitelist your local IP address. 

Finally, you can start up docker with the following command: 

.. code-block:: bash

    docker run --rm -it -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$ip:0 -p8888:8888 electronioncollider/escalate




**Credits**:

The EIC Container project is coordinated by 
`David Lawrence <mailto:davidl@jlab.org>`_ and `Dmitry Romanov <mailto:romanov@jlab.org>`_.
