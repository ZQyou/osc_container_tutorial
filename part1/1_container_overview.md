# Overview of Containers

### Download pre-built images
```shell
# Docker Hub
$ singularity pull docker://ubuntu:18.04

# Singularity Hub
$ singularity pull shub://vsoch/hello-world

# Container Library
$ singularity search lolcow
$ singularity pull library://sylabsed/examples/lolcow
```

### Manage images
Cache folders
```shell
# using cache command
$ singularity cache list -a

# the default cache is in your home directory
$ ls ~/.singularity/cache/*

# clean cached images
$ singularity cache clean -a

```
Download a large image
```shell
# Use other file systems for caches, squashfs temp files and download

$ qsub -I -l nodes=1:ppn=1 
$ cd $TMPDIR 
$ export SINGULARITY_CACHEDIR=$TMPDIR 
$ export SINGULARITY_TMPDIR=$TMPDIR 
$ singularity pull docker://qiime2/core:2019.1
$ cp qiime2_core_2019.1.sif /where/to/keep/image/
```
