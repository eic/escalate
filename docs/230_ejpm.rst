:orphan:

EJPM
----

`Detailed EJPM documentation <https://gitlab.com/eic/ejpm>`_

Installation
............


ejpm is EIC software centric package/build manager. It is the designed
to be the default tool to build G4E on users machine, as it helps with:

-  building dependent packages (with "right" compilation flags)
-  setup environment variables to run everything
-  what packages to install by system packet manager
-  rebuild/update/remove/clean existing packages

    Still, ejpm is not a requirement.

First, install ejpm itself:

.. code:: bash

    pip install --user ejpm

(If you have certificate problems (JLab issue), don't have pip, or have
other problems, `here is the detailed documentation <https://gitlab.com/eic/ejpm>`__ )


Install g4e and possible other EIC packets (ejana, eic-smear, etc.)

.. code:: bash

    # 1. System prerequesties
    ejpm req centos g4e      # get list of required OS packets. Use `ubuntu` on debian  
    sudo yum install ...     # install watever 'ejpm req' tells you

    # 2. Where to install
    ejpm --top-dir=<where-to>   # Directory where packets will be installed

    # 3. Install
    ejpm install g4e            # install 'Geant 4 EIC' and dependencies (like vgm, hepmc)

    # 4.  Source environment
    source ~/.local/share/ejpm/env.sh  # Use *.csh file for tcsh


User packages
.............


If you have ROOT and Geant4 and don't want EJPM to build them, here is how to use your packages with ejpm:

.. code:: bash

    # Before running 'ejpm install g4e'
    ejpm set root `$ROOTSYS`    # Path to ROOT installation
    ejpm set geant <path>       # Path to Geant4 installation   

Hint (!). Run ejpm to overview all installed packets, environment and
status by 'ejpm' command

Here is the sample output:

::

    > ejpm

    EJPM v0.01.19
    top dir :
        /eic
    state db :
        ~/.local/share/ejpm/db.json  (users are encouraged to inspect/edit it)
    env files :
        ~/.local/share/ejpm/env.sh
        ~/.local/share/ejpm/env.csh

    INSTALLED PACKETS: (*-active):
     vgm:
        * /eic/vgm/vgm-v4-5 (owned) 
     root:
        * /eic/root/root-v6-16-00 (owned)
     geant:
          /eic/geant/geant-v10.5.0 (owned)
        * /eic/geant4-10.6-betta
     hepmc:
        * /eic/hepmc/hepmc-HEPMC_02_06_09 (owned) 
     g4e:
        * /eic/g4e/g4e-dev (owned)



Switch software versions
........................


.. code:: bash

    # ejpm config <package> branch <version>
    ejpm config g4e branch v1.3.8
    # or
    ejpm config g4e branch master
    # now install a new version
    ejpm install -f g4e

To check packet configuration:

.. code:: bash
    
    ejpm config g4e

To check or change global configuration (for all packages)

.. code:: bash
    
    ejpm config global      # prints version
    ejpm config global cxx_version=17


.. warning:: if you install a new version of package EJPM doesn't rebuild/reinstall downstream packages.

This means that if you install additional version of g4e you don't have to do anything, as there is no packages depending on g4e. G4E is on top. 
But if you install a different version of ROOT or ACTS you have to rebuild packages, that depend on it. That is EJPM weakness. 


 


