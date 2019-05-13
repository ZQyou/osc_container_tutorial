# Build a Container

Check the version of Singularity
```
$ singularity version
3.1.0-1
```

```shell
$ apt update -y
$ apt install -y wget gcc make libbz2-dev zlib1g-dev \
  libncurses5-dev libncursesw5-dev liblzma-dev
# clean up
$ apt autoclean
$ apt autoremove --purge -y
$ rm -rf /var/lib/apt/lists/*
```

Commonly shared file systems:
`$HOME` (`/root`) , `/tmp` , `/proc` , `/sys` , `/dev`, and `$PWD` are among the system-defined bind paths.


## Install software 1
```shell
$ sudo singularity build samtools_1.7.sif samtools_1.def
$ ./samtools_1.7.sif --version
```

## Install software 2
```shell
$ sudo singularity build samtools_1.9.sif samtools_2.def
$ ./samtools_1.9.sif --version
```

## Install software 3 
```shell
$ mkdir -p /tmp/github.com
$ pushd /tmp/github.com
$ git clone https://github.com/samtools/samtools.git
$ cd samtools
$ git clone https://github.com/samtools/htslib.git
$ popd
$ export SINGULARITYENV_SAMTOOLS_DEV=/tmp/github.com/samtools
$ sudo -E singularity build samtools_dev.sif samtools_3.def
$ ./samtools_dev.sif --version
```
