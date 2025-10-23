# UBC NLP Servers
Our lab has 3 servers with a total of 6 GPUs. Access to these GPUs are restricted to only members of our group.  
This document will walk you through steps to [obtain access](#obtaining-access) to our servers, details about the [file system](#file-system), as well as providing you with some of [my experiences](#personal-experiences) using these compute clusters.

## Getting Access
1. TODO: get access. Our servers have addresses `ubc-nlp-gpu1`, `ubc-nlp-gpu2` and `ubc-nlp-gpu3`.
2. To login to our compute servers, you will need to proxy jump from UBC Remote server. On command line, this will be `ssh -J CWL@remote.cs.ubc.ca CWL@ubc-nlp-gpu1`.
3. (Optional) if you want to avoid entering your password each time you log in, consider [adding your ssh key](technical/ssh_key.md) to `remote.cs.ubc.ca`.

## File System
Our storage directory is in `/ubc/cs/research/nlp-raid/students/CWL/`. Please be reminded to consistently deleting unused files, as we often run out of storage. The old directory `/ubc/cs/research/nlp/CWL/` had ran out of space.

## Personal Experiences