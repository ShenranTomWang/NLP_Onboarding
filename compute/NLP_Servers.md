# UBC NLP Servers
Our lab has 3 servers with a total of 6 GPUs. Access to these GPUs are restricted to only members of our group.  
This document will walk you through steps to [obtain access](#obtaining-access) to our servers, details about the [file system](#file-system), as well as providing you with some of [my experiences](#personal-experiences) using these compute clusters.

## Getting Access
1. To obtain access, email the help desk at [help@cs.ubc.ca](help@cs.ubc.ca) and CC your supervisor. You will need access to [remote.cs.ubc.ca](remote.cs.ubc.ca) and our servers with addresses `ubc-nlp-gpu1`, `ubc-nlp-gpu2`, `ubc-nlp-gpu3` and `ubcml-nlp`.
2. To login to our compute servers, you will need to proxy jump from UBC Remote server. On command line, this will be `ssh -J CWL@remote.cs.ubc.ca CWL@ubc-nlp-gpu1`. Alternatively, you can first `ssh CWL@remote.cs.ubc.ca` and then do `ssh CWL@ubc-nlp-gpu1` there. To configure your ssh config file, see the [configuration section](#ssh-configuration).
3. (Optional) you are given 10GB storage upon approval of access to the cluster. If you want more storage, email the help desk at [help@cs.ubc.ca](help@cs.ubc.ca) and CC your supervisor to get allocation under `/ubc/cs/research/nlp-raid/students`.
4. (Optional) if you want to avoid entering your password each time you log in, consider [adding your ssh key](../technical/ssh_key.md) to `remote.cs.ubc.ca`.

## SSH Configuration
You can setup your ssh config list this:
```
Host UBC-Remote-Research
    HostName remote.cs.ubc.ca
    User shenranw
    ForwardX11 yes
Host UBC-NLP-Lab-GPU1
    HostName ubc-nlp-gpu1
    User shenranw
    ProxyJump UBC-Remote-Research
    ForwardX11 yes
Host UBC-ML-NLP
    HostName ubcml-nlp
    User shenranw
    ProxyJump UBC-Remote-Research
    ForwardX11 yes
```
Now `ssh -J CWL@remote.cs.ubc.ca CWL@ubc-nlp-gpu1` becomes `ssh UBC-NLP-Lab-GPU1`.

## System Specs
- `ubc-nlp-gpu1`: TODO: how many GPUs? Specs?
- `ubc-nlp-gpu2`: TODO: how many GPUs? Specs?
- `ubc-nlp-gpu3`: 4 RTX A6000 (48GB), 2 RTX 6000 Ada Generation (48GB)
- `ubcml-nlp`: 1 RTX A5000 (24 GB). TODO: provide more information once I log in there, e.g. using Slurm?

## File System
Our storage directory is in `/ubc/cs/research/nlp-raid/students/CWL/`. Please be reminded to consistently deleting unused files, as we often run out of storage. The old directory `/ubc/cs/research/nlp/CWL/` had ran out of space.

## Personal Experiences