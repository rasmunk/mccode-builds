=============
mcstas-builds
=============

A set of playbooks for creating container images for the folliwing packages

- mcstas/mcrun `Mcstas <https://github.com/McStasMcXtrace/McCode>`_
- mcxtrace/mxrun `Mcxtrace <https://github.com/McStasMcXtrace/McCode>`_
- mcstas/mccxtrace/mcrun/mxrun `McCode <https://github.com/McStasMcXtrace/McCode>`_

The images are created with `ansible-bender <https://github.com/ansible-community/ansible-bender.git>`_,
which utilizes `buildah <https://github.com/containers/buildah>`_ to ensure that the images
can be scheduled with `Docker <https://www.docker.com/>`_ or `podman <https://github.com/containers/libpod>`_.

---------------
Getting Started
---------------
To begin with, ensure that you have `ansible-bender` properly installed so that it can be executed from the shell.
Afterwards it is simply a matter of cloning the source::

    git clone https://github.com/rasmunk/mccode-builds

-------------
Example build
-------------

To build the general mccode image::

    ansible-bender build plays/containers/builds/mccode/mccode.yml

By default the temporary build files are being written to the ``/tmp`` folder, this can be changed by defining the `TMPDIR` environment variable::

    export TMPDIR=$HOME/my_tmp_folder

This will write the build files to ``$HOME/my_tmp_folder`` during the build instead of `/tmp`.

------------
Public Image
------------

By default, the built images are published at the DockerHub registry at the `nielsbohr <https://hub.docker.com/r/nielsbohr/>`_ profile.

For instance the ``mcode.yml`` build, is published as the `mcstas-mxtrace <https://hub.docker.com/r/nielsbohr/mcstas-mcxtrace>`_ image.

-----------
Example Run
-----------

Anything that is in the containers shell PATH can be executed as a command parameter. For instance if we want to run an mxrun example, it can simply be accomplished by the following command::

    docker run nielsbohr/mcstas-mcxtrace:latest mxrun /usr/local/share/examples/MAXII_711.instr
    
The ``mxrun`` command here functions exactly as you would normally expect. For instance we can postfix the instrument arguments to the command::

    docker run nielsbohr/mcstas-mcxtrace:latest mxrun /usr/local/share/mcxtrace/examples/MAXII_711.instr \
    R=-100 phi_mirror=3 phi_mono=9.25 chi=0 ome=0 phi=0 tth=0
