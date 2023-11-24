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

Singularity version 3.x creates a container image file called HALFpipe_{version}.sif in the directory where you run the pull command. For Singularity version 2.x the file is named halfpipe-halfpipe-master-latest.simg. Whenever you want to use the container, you need pass Singularity the path to this file.

NOTE: Singularity may store a copy of the container in its cache directory. The cache directory is located by default in your home directory at ~/.singularity. If you need to save disk space in your home directory, you can safely delete the cache directory after downloading, i.e. by running rm -rf ~/.singularity. Alternatively, you could move the cache directory somewhere with more free disk space using a symlink. This way, files will automatically be stored there in the future. For example, if you have a lot of free disk space in /mnt/storage, then you could first run mv ~/.singularity /mnt/storage to move the cache directory, and then ln -s /mnt/storage/.singularity ~/.singularity to create the symlink.

Docker will store the container in its storage base directory, so it does not matter from which directory you run the pull command.

**Quality control (QC)**
--------------------------

After running the pipeline, an output folder will be created. If the pipeline ran successfully, your output folder should look like this:

**/Output** 
**|_reports** → this contains all the QC information 
**|_derivatives** → this contains the extracted features for each subject (from the CorrMatrix, DualReg, fALFF, ReHo, SeedCorr analyses), along with the confound file (confounds.tsv), the preprocessed image(s) (preproc.nii.gz) and the mask_file.nii.gz 
**|_nypipe**  → this contains the intermediate pre-processing files. When using the standard pipeline, not all intermediate images are saved to save space. However you can choose to save everything by changing the flag: --keep (more information can be found on GitHub 
**|_rawdata** → this folder contains the raw T1 images and epi in BIDS
**|_log.txt**
**|_err.txt**  
**_halfpipe.log.txt**
**|_spec.json**
|_ an execgraph and workflow file (you can ignore this)
|_possibly files starting with ‘crash’

The files important for **QC** are in the **reports** folder. This contains:

* The web file **index.html**, which is the main web page that you will use to perform quality control (see below)
* **reportvals.txt** → this is a group file that contains the mean of the quality metrics (aroma_noise_frac, the fd_gt_0_5, mean_fd, mean_gm_tsnr) for each subject
* **reportpreproc.txt** → this is a group file that reports the status of the pre-processing (done/missing) of the resting state image for each subject
* In the reports folder there are also individual subject folders (that contain the images used to create the index.html and other files .js and .json.lock. You don’t have to worry about these files.

**Note:** you can copy the QC folder (reports) anywhere (e.g., on a local machine) as long as you copy the entire reports folder. The reports folder will take ~10 MB of space per subject plus 10 MB for each functional image. So if each subject has just the resting state, it would take ~20 MB per subject.

Important files for troubleshooting:

* The **log.txt** file contains the record of all the steps performed by the pipeline when it was running. Checking the log will help you troubleshoot if you run into any problems.
* The **err.txt file** contains the record of the errors
* The **crash files** might contain information about processes that crashed. If you submit an issue on GitHub, please include this file.



