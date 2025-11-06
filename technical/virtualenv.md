# Virtual Env Tutorial
[Virtual Env](https://docs.python.org/3/library/venv.html) is python's built-in environment manager. In this tutorial I will walk you through how to [create a venv](#create-a-venv)

## When to use `venv`
1. Certain clusters ([Compute Canada](../compute/Compute_Canada.md)) do not allow using `conda`.
2. All packages you require are pythonic. That is, your project only uses python. Venv provides a environment with less storage usage than other methods.

## When to not use `venv`
1. You are compiling other languages than python.
2. Packages you need require building with other languages in which are not included in the cluster's available softwares. In this case you may need to use `conda` or `apptainer`.

## Create a `venv`
```shell
ENVDIR="directory/you/want/to/store/your/environment"
python -m venv ${ENVDIR}
source ${ENVDIR}/bin/activate
```
You can then setup your `venv` with `pip install`.