# Overview of Containers

### Download pre-built images
From Docker hub
```shell
singularity pull docker://ubuntu:18.04
```
From Singularity Hub
```shell
singularity pull shub://singularityhub/hello-world
```
From Singularity Library
```shell
singularity search lolcow
singularity pull library://library/default/lolcow
```

### Manage images
Cache folders
```shell
# using cache command
> singularity cache list -v

# the default cache is in your home directory
> ls ~/.singularity/cache/*

# clean cached images
> singularity cache clean

```
Download a large image
```shell
# Use other file systems for caches, squashfs temp files and download=
> sinteractive -n 1
> cd $TMPDIR 
> export SINGULARITY_CACHEDIR=$TMPDIR 
> export SINGULARITY_TMPDIR=$TMPDIR 
> singularity pull docker://qiime2/core:2019.1
> cp qiime2_core_2019.1.sif /where/to/keep/image/
```
