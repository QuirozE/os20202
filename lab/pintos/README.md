# Rough translation of the installation guide

## QEMU

### Installation

By default, pintOS runs on [QEMU](https://www.qemu.org/). It is what will be
used.

It requires the ``qemu-system-i386`` module to run.

In Arch, use

```bash
$ sudo pacman -Syu qemu qemu-arch-extra
$
```

In other distributions, use you prefered pakcage manager to install them, or
use the source code if unavailable.

### Configuration

pintOS requires direct access to the i386 architecture with the command
`qemu`, so the following symbolic link has to be created.

```console
$ sudo ln -s /usr/bin/qemu-system-i386 /usr/bin/qemu
$
```

## pintOS

### Building

First, download the source code in this repo.

The source code scripts must be accessible from any directory. The easiest way
to do this is by modifying the system `PATH`.

```bash
$ export PATH=$PATH:/<pintOS_source_code>/src/utils
$
```

And then, just build the source code using the Makefile in
[src/threads](src/threads/)

```bash
$ make
mkdir -p build/devices
mkdir -p build/filesys
mkdir -p build/lib
mkdir -p build/lib/kernel
mkdir -p build/lib/user
mkdir -p build/tests/filesys/base
mkdir -p build/tests/userprog
mkdir -p build/tests/userprog/no-vm
mkdir -p build/threads
mkdir -p build/userprog
cp ../Makefile.build build/Makefile
cd build && make all
...
```

[src/threads/build](src/threads/build) directory should appear

### Running

To check the build, from `src/threads` run the simplest example

```bash
$ pintos run alarm-single
...
qemu -hda /tmp/WKPd2L0TQK.dsk -m 4 -net none -serial stdio
WARNING: Image format was not specified for '/tmp/WKPd2L0TQK.dsk' and probing guessed raw.
         Automatically detecting the format is dangerous for raw images, write operations on block 0 will be restricted.
         Specify the 'raw' format explicitly to remove the restrictions.
PiLo hda1
Loading............
Kernel command line: run alarm-single
Pintos booting with 3,968 kB RAM...
367 pages available in kernel pool.
367 pages available in user pool.
Calibrating timer...  314,163,200 loops/s.
Boot complete.
Executing 'alarm-single':
(alarm-single) begin
(alarm-single) Creating 5 threads to sleep 1 times each.
(alarm-single) Thread 0 sleeps 10 ticks each time,
(alarm-single) thread 1 sleeps 20 ticks each time, and so on.
(alarm-single) If successful, product of iteration count and
(alarm-single) sleep duration will appear in nondescending order.
(alarm-single) thread 0: duration=10, iteration=1, product=10
(alarm-single) thread 1: duration=20, iteration=1, product=20
(alarm-single) thread 2: duration=30, iteration=1, product=30
(alarm-single) thread 3: duration=40, iteration=1, product=40
(alarm-single) thread 4: duration=50, iteration=1, product=50
(alarm-single) end
Execution of 'alarm-single' complete.
```

### Tests

Tests are programs. And as such they can be run as example programs, like
`alarm-single`.

The sintax is just `pintos run <test>`

However, the tests must produce a specific output. To check if the test is
performing correctly, ther is an in-built tool to compare output.

For example,

```bash
$ make build/tests/threads/alarm-single.result
cd build && make tests/threads/alarm-single.result
make[1]: Entering directory '<PINTOSPATH>pintos/src/threads/build'
pintos -v -k -T 60 --qemu  -- -q  run alarm-single < /dev/null 2> tests/threads/alarm-single.errors > tests/threads/alarm-single.output
perl -I../.. ../../tests/threads/alarm-single.ck tests/threads/alarm-single tests/threads/alarm-single.result
pass tests/threads/alarm-single
make[1]: Leaving directory '<PINTOSPATH>/pintos/src/threads/build'
```

The `pass` label signals that everything functions as it should.

The general sintax for this comparaison is `make build/tests/<section>/<test>.result`.

Several logging files are generated in `build/test/<section>/` to register any
incorrect behavior.

#### User Prog

User tests, as well as every non kernel program, need diskpace.

The easiest way to do this is by creating and deleting a disk in place.

For example, running the following inside `src/userprog`

```bash
$ pintos --filesys-size=2 -p build/tests/userprog/args-none -a args-none --  -f run 'args-none'
...
Copying build/tests/userprog/args-none to scratch partition...
qemu -hda /tmp/QTfJ3nhtDw.dsk -m 4 -net none -serial stdio
WARNING: Image format was not specified for '/tmp/QTfJ3nhtDw.dsk' and probing guessed raw.
         Automatically detecting the format is dangerous for raw images, write operations on block 0 will be restricted.
         Specify the 'raw' format explicitly to remove the restrictions.                                                                  PiLo hda1ing-prototypes -Wsystem-headers -Wno-nonnull-compare   -MMD 
Loading............
Kernel command line: -f extract run args-none
Pintos booting with 3,968 kB RAM...
367 pages available in kernel pool.
367 pages available in user pool.
Calibrating timer...  314,163,200 loops/s.
hda: 5,040 sectors (2 MB), model "QM00001", serial "QEMU HARDDISK"
hda1: 205 sectors (102 kB), Pintos OS kernel (20)
hda2: 4,096 sectors (2 MB), Pintos file system (21)
hda3: 123 sectors (61 kB), Pintos scratch (22)
filesys: using hda2
scratch: using hda3
Formatting file system...done.
Boot complete.
Extracting ustar archive from scratch device into file system...
Putting 'args-none' into the file system...
Erasing ustar archive...
Executing 'args-none':
(args) begin
(args) argc = 1
(args) argv[0] = 'args-none'
(args) argv[1] = null
(args) end
args-none: exit (0) 
Execution of 'args-none' complete.
```

This will show some additional lines, but the most of the output will stay the
same.

Breaking down each step

* `--filesys-size`: size of disk to create in megabytes
* `-p`: path in local disk to the source file. This file will be copied.
* `-a`: new file name inside the new disk.
* `--`: marks end of emulator args and begining of program args.
* `-f`: new disk will be formated before using it.
