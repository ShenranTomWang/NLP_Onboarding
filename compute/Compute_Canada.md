# Compute Canada Tutorial
Compute Canada is a funded by the federal government and provides access to High-Performance Compute for researchers in Canada. You may find its documentation [here](https://docs.alliancecan.ca/wiki/Technical_documentation).  
This document will walk you through steps to [obtain access](#obtaining-access) to compute clusters on Compute Canada, details of the [file system](#file-system), as well as providing you with some of [my experiences](#personal-experiences) using these compute clusters. I will also go through some details of [using Slurm](#slurm-specs) in Compute Canada clusters.

## Obtaining Access
1. Go to [https://ccdb.alliancecan.ca/](https://ccdb.alliancecan.ca/) to register for your account. If you already have an account, log in to it.
2. If you just registered, skip this step. In you have an account and logged in, check your roles: if your current role is already with your current supervisor, skip this step. Otherwise, go to _My Account_ -> _Apply for a New Role_ and enter your supervisor's information there. You will need your supervisor to give you their _CCRI_.
3. An email will be sent to your supervisor to approve your access if you just registered or switched supervisor. Once approved, you can go to _Resources_ -> _Access Systems_ to gain access to compute servers. We will normally be using servers under _HPC_. Each server has different hardware. You can find details [here](https://docs.alliancecan.ca/wiki/Technical_documentation) under _Resources_ on the left panel.
4. (Optional) if your supervisor is affiliated with the [Vector Institute](https://vectorinstitute.ai/), you have access to [Killarney](https://docs.alliancecan.ca/wiki/Killarney). You can request access to Killarney under _Resources_ -> _Access Systems_ -> _Artificial Intelligence_.
5. Once you are granted access to compute servers, you can `ssh` into them with your _username_: `ssh username@address`. Server addresses can be found [here](https://docs.alliancecan.ca/wiki/Technical_documentation) under _Resources_ on the left panel.
6. (Optional) if you want to avoid entering your password each time you log in, consider [adding your ssh key to the server](../technical/ssh_key.md).

## File System
There will be two folders, `scratch` and `projects` in your home directory. Please keep all large files or environments in `scratch` folder.

## Personal Experiences
- Compute Canada is open to almost all researchers in Canada, meaning that there are many people competing over a small number of GPUs. The servers use [Slurm](../technical/slurm.md) to manage jobs, which could cause a very long wait time.
- Certain older servers (e.g. Narval) do not have internet in their compute nodes, meaning that when you submit a job, it runs without internet connection. However, newer servers (Fir, Nibi) now have internet connection in compute nodes.
- Setting up the environment could be very tricky as you are not allowed to use `conda`. Instead, they have pre-built wheels for python packages. To set up an environment, I recommend using `python`'s `virtualenv`:
```shell
module load StdEnv/2023     # In general this should be sufficient. If you require certain other compilers you can module load them manually
ENVDIR="directory/you/want/to/store/your/environment"
virtualenv --no-download ${ENVDIR}
source ${ENVDIR}/bin/activate
pip install --no-index requirements.txt     # Using --no-index to install pre-built wheels. Since the environment here is less customizable, always installing from the web may cause conflicts
```
- (Not recommended) in certain scenarios where the above `virtualenv` setup cannot meet your requirements, you can use [Apptainer](../technical/apptainer.md).

## Slurm Specs
For basic usage of Slurm, checkout the [Slurm document](../technical/slurm.md). For Compute Canada clusters, you can use `sq` to see status of all your jobs. to start an interactive session, use:
```shell
salloc --time=4:0:0 --mem-per-cpu=16G --ntasks-per-node=8 --gpus-per-node=a100:1
```
Below is a template job script for Compute Canada clusters:
```shell
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --gpus-per-node=a100:1
#SBATCH --ntasks-per-node=8
#SBATCH --mem=24G
#SBATCH --time=1-00:00
#SBATCH --account=def-xxxxxx    # Use your supervisor's username
module load ...
source .../bin/activate
...
```