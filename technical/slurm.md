# Slurm Tutorial
[Slurm](https://slurm.schedmd.com/documentation.html) is a CLI workload manager that manages queues of submitted jobs.  
In this document, I will walk you through some [basic usage](#basic-usage) of Slurm.

## Basic Usage
Most common ussecases are listed below:
- Submitting a job: use `sbatch job.sh` to submit a job. Your job.sh should be organized to contain configurations according to each server's requirements. I have given examples of job scripts for each platform in their corresponding documents.
- Monitoring a job: use `squeue` to monitor a job. To see all your jobs of a user, use `squeue -u <username>`. to see all running jobs of a certain partition (i.e. hardware requirements), use `squeue -p <partition>`. Example: `squeue -p a100`.
- Cancelling a job: to cancel a job, use `scancel <job-id>`.
- Interactive session: Each platform have different variants to start an interactive session. Checkout each platform's document for this information.