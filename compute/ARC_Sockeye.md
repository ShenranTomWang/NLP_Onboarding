# ARC Sockeye Tutorial
ARC Sockeye is a High-Performance computing platform available to UBC researchers only. You must have a UBC CWL to use this platform. [UBC myVPN](https://it.ubc.ca/services/email-voice-internet/myvpn) is required to log in to the server if you are not connected to `ubcsecure`.  
This document will walk you through [Getting Access](#getting-access) to the ARC Sockeye compute cluster, details of the [cluster](#system-specs) and [file system](#file-system), as well as some of [my experiences](#personal-experiences) with this cluster.

## Getting Access
1. To get access, contact your supervisor so they can reach out to ARC Sockeye.
2. Once you obtained access, follow instructions [here](https://it.ubc.ca/services/email-voice-internet/myvpn) to setup UBC myVPN.
3. Turn on your UBC myVPN if you are not connected to `ubcsecure`. you can connect to sockeye at `sockeye.arc.ubc.ca` with your CWL. So `ssh cwl@sockeye.arc.ubc.ca`.
4. You can manage your jobs at [ARC Ondemand](https://ondemand.arc.ubc.ca/). Documentation is available [here](https://confluence.it.ubc.ca/spaces/UARC/pages/168841664/Using+Sockeye).
4. (Optional) if you want to avoid entering your password each time you log in, consider [adding your ssh key to the server](../technical/ssh_key.md).

## System Specs
You have access to V100-32G and V100-16G GPUs on Sockeye. By default you have no access to the internet in batch jobs, but you can enable internet access via `module load http_proxy`.

## File Systems
You have a limited space at your home directory, so I recommend you to store your environments and large files in your `scratch` which can be found at `/scratch/{supervisor-allocation-name}/`. It is also worth-notice that when you run a Slurm job, `/scratch` is the only place where the job will have write permission, so always save things to `/scratch` when you run a batch job.

## Personal Experiences
- Although ARC Sockeye uses [Slurm](../technical/slurm) to queue jobs, there are not a lot of people competing for resources, so I normally get my allocation as soon as I request it.
- A drawback compared to other platforms is that ARC Sockeye only have V100s, which is slower and has smaller memory.
- You are recommended to use `conda` to set up your environments.

## Slurm Specs
You may only submit jobs in `/scratch` on Sockeye.
For basic usage of Slurm, checkout the [Slurm document](../technical/slurm.md). To start an interactive session, use:
```shell
salloc --time=4:0:0 --mem-per-cpu=16G --ntasks=1 --nodes=1 --gpus=1 --constraint=gpu_mem_32 --account=xxxxxx-gpu
```
Below is a template job script for ARC Sockeye:
```shell
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --gpus=1
#SBATCH --ntasks=4
#SBATCH --mem=24G
#SBATCH --time=2-00:00:00
#SBATCH --account=xxxxxx-gpu
#SBATCH --constraint=gpu_mem_32
#SBATCH --output=output_logging_file.log
#SBATCH --error=error_logging_file.log
#SBATCH --mail-user=your@e.mail
#SBATCH --mail-type=ALL
#SBATCH --job-name=job_name
...
```
For more help, see the [official documentation](https://confluence.it.ubc.ca/spaces/UARC/pages/318409964/Running+Jobs)

## Softwares
Like any high-performance computing clusters, Sockeye has prepared commonly used compilers (cuda, gcc, etc.) and other modules for you. You may load them using:
```shell
module load {module-name}
```
Details are available at the [software information page](https://confluence.it.ubc.ca/spaces/UARC/pages/187507341/Software).