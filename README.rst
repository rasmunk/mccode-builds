=============
mcstas-builds
=============

A set of playbooks for creating container images for the folliwing packages

- mcstas/mcrun (https://github.com/McStasMcXtrace/McCode)
- mxxtrace/mxrun (https://github.com/McStasMcXtrace/McCode)

The images are created with `ansible-bender <https://github.com/ansible-community/ansible-bender.git>`_,
which utilizes `buildah <https://github.com/containers/buildah>`_ to ensure that the images
can be scheduled with `Docker <https://www.docker.com/>`_ or `podman <https://github.com/containers/libpod>`_.

---------------
Getting Started
---------------
To begin with, ensure that you have `ansible-bender` properly installed so that it can be executed from the shell.
Afterwards it is simply a matter of cloning the source.

    git clone https://github.com/rasmunk/mcstas-builds

-------------
Example build
-------------

To build the mcxtrace image:

    ansible-bender build plays/containers/builds/mcxtrace/mcxtrace.yml

By default the temporary build files are being written to the `/tmp` folder, this can be changed by defining the `TMPDIR` environment variable:

    export TMPDIR=$HOME/my_tmp_folder

This will write the build files to `$HOME/my_tmp_folder` during the build instead of `/tmp`.