============================================
**ENIGMA HALFpipe Quality Control manual**
============================================

Version 2 —— 2023-04-19
-----------------------

*Written by Lina Mograby*
*Previous version by Elena Pozzi, Yara Toenders, Ilya Veer, Lea Waller, Courtney Haswell, Rajendra Morey, and Lianne Schmaal*

Please address questions and comments to enigma@charite.de


1. Install a container platform
---------------------------------

HALFpipe is contributed as a container, meaning that all required software comes bundled in a monolithic file, the container. This allows for easy installation on new systems, and makes data analysis more reproducible, because software versions are guaranteed to be the same for all users. 

The first step is to install one of the supported container platforms. If you are using a high-performance computing cluster, more often than not `Singularity <https://sylabs.io/>`_ will already be available.

If not, we recommend using the latest version of `Singularity <https://sylabs.io/>`_. However, it can be somewhat cumbersome to install, as it needs to be built from source. 

The `NeuroDebian <https://neuro.debian.net/>`_ package repository provides an older version of `Singularity <https://sylabs.io/>`_ for `some <https://neuro.debian.net/pkgs/singularity-container.html>`_ Linux distributions.

If you are running mac OS, then you should be able to run the container with Docker Desktop.

If you are running Windows, you can also try running with Docker Desktop, but we have not done any compatibility testing yet, so issues may occur, for example with respect to file systems. 

==================== ========== ================================================================
Container platform   Version    Installation
==================== ========== ================================================================
Singularity          3.x         https://sylabs.io/guides/3.8/user-guide/quick_start.html
-------------------- ---------- ----------------------------------------------------------------
Singularity          2.x        sudo apt install singularity-container
-------------------- ---------- ----------------------------------------------------------------
Docker                          see https://docs.docker.com/engine/install 
==================== ========== ================================================================

