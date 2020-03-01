# Schedule
In this lab work, a priority-based scheduler is implemented.

To do this, all the processes are inserted in the ready list according to their
priorities.

And at each priority change in a process, the list must be reordered.

This gives linear insertion and constant queries.

## Buil and run
The necessary changes are included in [patch/](patch/).

Move to the directory and use

```console
$ git am *.patch
```

Then, follow the instruction in [README.md](../pintos/README.md) to build and 
run the modified pintOS.

## Extra

As an extra credit, the priority is implemented using an array of lists, one per
priority. This gives insertion and queries both in constant time

The additional modifications are in [patch/extra](patch/extra/).

To apply them, first the base patches must be applied.

## Tests
To check functionality, use the following command to run test

```console
$ pintos run <test>
```
In this case, the pertinent tests are

* prority-fifo
* priority-preempt
* priority-change