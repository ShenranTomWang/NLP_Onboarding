# Slurm Tutorial
[Slurm](https://slurm.schedmd.com/documentation.html) is a CLI workload manager that manages queues of submitted jobs.  
In this document, I will walk you through some [basic concepts](#basic-concept) and [basic usage](#basic-usage) of Slurm.

## Basic Concept
Once you log in to a cluster with Slurm, you are allocated a basic cpu for managing your files (login node), etc. Notice that this cpu allocation is only designed for lightweight executions such as managing the file system and running the VSCode server, and not running any compute-heavy operations. If you want access to a compute node (which could potentially contain a GPU), you will need to use Slurm.  
When you obtain a compute node with Slurm, you will obtain access to your specified hardware (e.g. GPUs). It is worth noticing that even if the cluster itself has GPUs, you will not be able to see them in the login node. You will only be exposed to the specified hardware upon approval of your Slurm request.

## Basic Usage
Most common ussecases are listed below:
- Submitting a job: use `sbatch job.sh` to submit a job. Your job.sh should be organized to contain configurations according to each server's requirements. I have given examples of job scripts for each platform in their corresponding documents.
- Monitoring a job: use `squeue` to monitor a job. To see all your jobs of a user, use `squeue -u <username>`. to see all running jobs of a certain partition (i.e. hardware requirements), use `squeue -p <partition>`. Example: `squeue -p a100`.
- Cancelling a job: to cancel a job, use `scancel <job-id>`.
- Interactive session: Each platform have different variants to start an interactive session. Checkout each platform's document for this information.