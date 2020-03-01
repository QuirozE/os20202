# Rough translation of the installation guide

## QEMU

### Installation

By default, pintOS runs on [QEMU](https://www.qemu.org/). It is what will be 
used.

It requires the ``qemu-system-i386`` module to run. 

In Arch, use 

```console
$ sudo pacman -Syu qemu qemu-arch-extra
```

In other distributions, use you prefered pakcage manager to install them, or 
use the source code if unavailable.

### Configuration

pintOS requires direct access to the i386 architecture with the command 
``qemu``, so the following symbolic link has to be created.

```console
$ ln -s /usr/bin/qemu-system-i386 /usr/bin/qemu
```

## pintOS

### Building

First, download the source code in this repo.

The source code scripts must be accessible from any directory. The easiest way
to do this is by modifying the system ``PATH``.

```console
$ export PATH=$PATH:/<pintOS_source_code>/src/utils
```

And then, just build the source code using the Makefile in 
[src/threads](src/threads/)

```console
$ make
```

[src/threads/build](src/threads/build) directory should appear

### Running

To check the build, from [src/threads](src/threads/) run the simplest example

```console
$ pintos run alarm-single
```

Then, to check the system is properly shutting down, run 

```console
$ pintos -- -q run alarm-single
```


