# Argument Passing

In this lab work, argument passing for user programs is implemented.

All the arguments are manually copied from the input string into the user stack.

## Build and run

The changes are coded as patches at `/patches`. To apply them use the following
inside directory.

```bash
$ git am *patch
Applying: Adding debbugin print, nothing is implemented yet
Applying: Adding aux fn, main problem still to implement
Applying: Adding first solution, not testes
Applying: Valid argument values in stack, can\'t test anything else until filename is split into words
Applying: Removing noisy spaces
Applying: Ignoring args while naming thread
Applying: Deleteing commented blocks and fixing typos
```

 And run the system normally.

## Tests

The pertinent tests in this labwork are

* `args-none`
* `args-sigle`
* `args-multiple`
* `args-many`
* `args-dbl.space`

All should be runned with diskspace.
