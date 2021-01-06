Local isntallation
==================

There are several ways how one can install packages locally:

1. Spack package manager
2. EJPM package manager
3. Combined Conda+EJPM isntallation
4. Manual build

What packet manager to use? 

EJPM was designed with user laptops/workstations and devlopment in mind. The intention of EJPM is to be a user friendly CLI alternative to "build scritps" that compiles chains of packages with right flags.
Spack is a full featured multi-platform package manager designed for clusters and super computers. It is possible to install software on laptops with Spack but at this point it is more prone to compilation errors. 

**Thus the recommendation is**: to use EJPM for personal laptops with Linux OS for personal use and development. Use Spack on farms or if you are familiar with Spack, use Spack for other projects, etc.

There is also a hybrid variant of using Conda+EJPM where Conda is used to download binaries of compilers, big packages like CERN ROOT and Geant4 and then EJPM is used to build EIC applications on top of it. 
This type of installation also guarantee a consistency with compillers, binary libraries, etc.

Here is the short comparison table between Spack and EJPM:

.. Table with EJPM vs Spack comparison

.. raw:: html
   :file: 202_ejpm_vs_spack_table.html


:ref:`spack-ejpm-comparison`.

.. include:: 230_ejpm.rst

.. include:: 240_spack.rst
