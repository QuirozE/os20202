# Timer sleep
In this lab work, the busy-wait sleeping method is replaced by a timer sleeping.

## Buil and run
The necessary changes are included in [patch/](patch/).

Move to the directory and use

```console
$ git am *.patch
```

Then, follow the instruction in [README.md](../pintos/README.md) to build and 
run the modified pintOS.

## Tests
To check functionality, use the following command to run test

```console
$ pintos run <test>
```
In this case, the pertinent tests are

* alarm-single
* alarm-multiple
* alarm-simultaneous
* alarm-zero
* alarm-negative