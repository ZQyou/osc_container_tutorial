# Build a Container

Check the version of Singularity
```shell
$ singularity version
3.1.1-1
```

Commonly shared file systems:
`$HOME` (`/root`) , `/tmp` , `/proc` , `/sys` , `/dev`, and `$PWD` are among the system-defined bind paths.

## Case 1
Use APT install: [samtools\_1.def](./samtools_1.def)
```shell
$ sudo singularity build samtools_1.7.sif samtools_1.def
$ ./samtools_1.7.sif --version
samtools 1.7
Using htslib 1.7-2
Copyright (C) 2018 Genome Research Ltd.

## use remote build
$ singularity build --remote samtools_1.7.sif samtools_1.def
```
## Case 2
Install from source code: [samtools\_2.def](./samtools_2.def)
```shell
$ sudo singularity build samtools_1.9.sif samtools_2.def
$ ./samtools_1.9.sif --version
samtools 1.9
Using htslib 1.9
Copyright (C) 2018 Genome Research Ltd.

## use remote build
$ singularity build --remote samtools_1.9.sif samtools_2.def
```

## Case 3
Install from source code with
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
