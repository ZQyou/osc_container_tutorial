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

### Manage images and caches
The defaul cache directories
```shell
ls ~/.singularity/cache/
```
List local cache
```shell
singularity cache list -v
```
Clean local cache
```shell
singularity cache clean
```

#### Download a large image
Request an interactive session
```shell
sinteractive -n 1
```
Use other file systems for caches, squashfs temp files and download
```shell
cd $TMPDIR 
export SINGULARITY_CACHEDIR=$TMPDIR 
export SINGULARITY_TMPDIR=$TMPDIR 
singularity pull docker://qiime2/core:2019.1
cp qiime2_core_2019.1.sif /where/to/keep/image/
```
