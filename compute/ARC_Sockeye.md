# ARC Sockeye Tutorial
ARC Sockeye is a High-Performance computing platform available to UBC researchers only. You must have a UBC CWL to use this platform. [UBC myVPN](https://it.ubc.ca/services/email-voice-internet/myvpn) is required to log in to the server.  
This document will walk you through [Getting Access](#getting-access) to the ARC Sockeye compute cluster, details of the [file system](#file-system), as well as some of [my experiences](#personal-experiences) of this cluster.

## Getting Access
1. To get access, contact your supervisor so they can reach out to ARC Sockeye.
2. Once you obtained access, follow instructions [here](https://it.ubc.ca/services/email-voice-internet/myvpn) to setup UBC myVPN.
3. Turn on your UBC myVPN, you can connect to sockeye at `sockeye.arc.ubc.ca` with your CWL. So `ssh cwl@sockeye.arc.ubc.ca`.
4. (Optional) if you want to avoid entering your password each time you log in, consider [adding your ssh key to the server](technical/ssh_key.md).

## File Systems
You have a limited space at your home directory, so I recommend you to store your environments and large files in your `scratch` which can be found at `/scratch/{supervisor-allocation-name}/`.

## Personal Experiences
- Although ARC Sockeye uses [Slurm](technical/slurm) to queue jobs, there are not a lot of people competing for resources, so I normally get my allocation as soon as I request it.
- A drawback compared to other platforms is that ARC Sockeye only have V100s, which is slower and has smaller memory.
- You are recommended to use `conda` to set up your environments.

## Slurm Specs
For basic usage of Slurm, checkout the [Slurm document](technical/slurm.md). To start an interactive session, use:
```shell
salloc --time=4:0:0 --mem-per-cpu=16G --ntasks=1 --nodes=1 --gpus=1 --constraint=gpu_mem_32 --account=xxxxxx-gpu
```
Below is a template job script for ARC Sockeye:
```shell
#!/bin/bash
#SBATCH --job-name=...
#SBATCH --account=xxxxxx-gpu
#SBATCH --time=3-00:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --mem=32G
#SBATCH --gpus=1
#SBATCH --constraint=gpu_mem_32
...
```