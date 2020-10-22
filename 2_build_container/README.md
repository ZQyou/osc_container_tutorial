# Build a Container

[Prerequisites](../Prerequisties.md)

Check Singularity version
```shell
singularity version
```

Commonly shared file systems:
`$HOME` (`/root`) , `/tmp` , `/proc` , `/sys` , `/dev`, and `$PWD` are among the system-defined bind paths.

## Building containers from writable `--sandbox` directories
### Pick a base container to create a sandbox
```shell
singularity build --sandbox ubuntu_18.04 docker://ubuntu:18.04
ls ubuntu_18.04
```
### Make changes inside the base container
```shell
sudo singularity shell --writable ubuntu_18.04
Singularity> pwd
/root
Singularity> apt update -y && apt install -y samtools
Singularity> apt autoclean && apt autoremove --purge -y
Singularity> rm -rf /var/lib/apt/lists/*
Singularity> exit
```
### Build your container 
```shell
sudo singularity build samtools_1.7.sif ubuntu_18.04
```
Test the image
```shell
singularity exec samtools_1.7.sif samtools --version
```
```
samtools 1.7
Using htslib 1.7-2
Copyright (C) 2018 Genome Research Ltd.
```
### Update the container [samtools\_upd.def](./samtools_upd.def)
```shell
$ sudo singularity build --update ubuntu_18.04 samtools_upd.def
$ sudo singularity build samtools_1.7.sif ubuntu_18.04
$ ./samtoos_1.7.sif --version
$ singularity ./samtools_1.7.sif exec gcc --version
```

## Building containers from the Singularity definition files

### Case 1
Use APT install: [samtools\_1.def](./samtools_1.def)
```shell
$ sudo singularity build samtools_1.7.sif samtools_1.def
$ ./samtools_1.7.sif --version
samtools 1.7
Using htslib 1.7-2
Copyright (C) 2018 Genome Research Ltd.

## use remote build (for unprivileged user)
$ singularity build --remote samtools_1.7.sif samtools_1.def
```
### Case 2
Install from source code: [samtools\_2.def](./samtools_2.def)
```shell
$ sudo singularity build samtools_1.9.sif samtools_2.def
$ ./samtools_1.9.sif --version
samtools 1.9
Using htslib 1.9
Copyright (C) 2018 Genome Research Ltd.

## use remote build (for unprivileged user)
$ singularity build --remote samtools_1.9.sif samtools_2.def
```

### Case 3
Install from source code with pre-defined path: [samtools\_3.def](./samtools_3.def)
```shell
$ mkdir -p /tmp/dev
$ pushd /tmp/dev
$ wget https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2
$ tar xf samtools-1.9.tar.bz2
$ popd
$ export SINGULARITYENV_SAMTOOLS_DEV=/tmp/dev/samtools-1.9
$ sudo -E singularity build samtools_dev.sif samtools_3.def
$ ./samtools_dev.sif --version
samtools 1.9
Using htslib 1.9
Copyright (C) 2018 Genome Research Ltd.
```
