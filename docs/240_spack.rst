:orphan:

Spack
-----


Install spack
.............

Spack is a package management tool designed to support multiple versions
and configurations of software on a wide variety of platforms and
environments. Spack allows to automatically build target packages with
all needed dependencies. `Sapck
documentation <https://spack.readthedocs.io/en/latest/getting_started.html#installation>`__

The installation consist of 3 steps then: 1. Install spack itself 2.
Install EIC `repository <https://github.com/eic/eic-spack>`__ (with EIC
packages) 3. Run spack command to install g4e (or other packages)

To install spack and EIC repository:

.. code:: bash

    git clone https://github.com/spack/spack.git

    #Source environment

    # For bash/zsh users
    $ . spack/share/spack/setup-env.sh

    # For tcsh/csh users
    $ source spack/share/spack/setup-env.csh

You should be able now to use spack:

.. code:: bash

    spack info root

    (!) By default, all packages will be downloaded, built and installed
    in this spack directory

    `More documentation on spack
    installation <https://spack.readthedocs.io/en/latest/getting_started.html#installation>`__

Clone and add `eic-spack
repository <https://github.com/eic/eic-spack>`__:

.. code:: bash

    # Adding the EIC Spack Repository
    git clone https://github.com/eic/eic-spack.git

    # Add this repository to your Spack configuration
    spack repo add eic-spack

Example install and use g4e with spack
......................................

To install g4e with spack (this will install the latest stable version)

.. code:: bash

    spack install g4e

To install concrete version of spack:

.. code:: bash

    spack info g4e            # to see the available versions
    spack install g4e@1.3.7   # 

To see what is going to be installed/built

.. code:: bash

    spack speck -I g4e

To use G4E with spack:

.. code:: bash

    spack load g4e

    # or with exact version
    spack load g4e@1.3.7

`More documentation of spack
usage <https://spack.readthedocs.io/en/latest/basic_usage.html>`__


