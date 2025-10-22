# Apptainer Tutorial
This document will walk you through building and running an [Apptainer](https://apptainer.org/) environment in [Compute Canada](compute/Compute_Canada.md) servers.

## What is Apptainer?
Apptainer is a customized [Docker](https://www.docker.com/) environment that can be activated to run your experiments. It takes a pre-built docker image and convert it to a single `.sif` file.

## Why Apptainer?
Unlike in the native Compute Canada servers' environments, Apptainer has no restrictions of what packages can or cannot be installed. However, if you want to install a new dependency, you will also need to rebuild your docker image and the apptainer file, and from my experience Apptainer is extremely slow when you run it.

## Setup
1. On your laptop, use Docker to set up an Docker image and push it to the hub.
2. On the Compute Canada server, run:
```shell
module loa StdEnv/2023 apptainer/1.2.4
export APPTAINER_CACHEDIR="A/cache/dir/of/your/choice"
apptainer build name.sif docker://docker-image-url:version
```

## Running Apptainer Environment
You can run the apptainer environment with:
```shell
module loa StdEnv/2023 apptainer/1.2.4
export APPTAINER_CACHEDIR="A/cache/dir/of/your/choice"
apptainer run -C --nv --home "your/home/directory" -B "directory/you/want/to/add/to/apptainer/environment" -B "directory/you/want/to/add/to/apptainer/environment" name.sif bash "shell/script/to/execute"
```