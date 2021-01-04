
.. _spack-ejpm-comparison:

Detailed comparison between EJPM and Spack
==========================================


.. Table with EJPM vs Spack comparison

.. raw:: html
   :file: 016_ejpm_vs_spack_table.html

  
1. EJPM was designed with user laptops and work stations in mind to be a user friendly CLI alternative to "build scritps" that compiles compiling chains of packages with right flags. 
   Something that users can simply do `pip install ejpm; ejpm install package` EJPM was made. 
    
   Spack is a full featured multi-platform package manager designed for clusters and super computers. 
   Spack is capable to build and install multiple versions and configurations of software and shines here.
   It is possible to use spack on a laptop or a personal workstation also, but learning curve is steeper than with EJPM.


2. EJPM uses as much system packages as possible. E.g. EJPM have special command like `ejpm dep ubuntu` which lists all packages to be installed by your system package manager (yum, apt). 
   
   Contrary to this Spack tries to build as much dependent packages as possible. When building something like ROOT, Spack goes as deep as building its own Python, Perl, Mesa and even zip libraries. 
   That is the first major difference between EJPM and Spack. As the result EJPM uses less compilation time and dependencies are much less complicated but is much more dependent on what is installed and 
   configured in the system. On the other hand Spack is much more system independent, but building a lot of libraries takes much more time and more compilation error prone. 


3. To use packages ejpm users have to source an environment file which is re/generated every time EJPM configuration is updated. 
   It is possible to have different versions of packages but users have to control it manually. 
   
   Spack utilizes *modules* which is certainly more versatile 
   and sutable for large distributed systems (while works very well on workstations also). Spack uses rpath to link depencies between each other


4. Spack has large dependencies trees. Even if one flag is different between some packages it might try to build an alternative tree. Simply saying Spack tends to install many versions of ROOT or Geant4 packages
   and which takes large disk space and time. It is avoidable but requires additional care and supervision from user. 
   
   EJPM also allows to install new versions of a package but it doesn't check if it might
   affect downstream dependencies. That is kind of great disadvantage of EJPM compared to Spack.

   There is no automatic updates both in Spack and EJPM. Idea of Spack is that you just install a new version (and it installs all needed/updated dependencies).
