This project holds two simple utilities that are useful to test command-line
tools such as compiler in a convenient way. They are written in pure OCaml and
should work on any Unix platform that supports the base OCaml system.

To compile, assuming ocamlbuild is installed, just type `make`.

# Description

All the utilities can deal with multiple files as command-line arguments.

## split utility

Usage: `split FILE.split` cuts FILE.split into multiple parcels, each of them
stored within a new file. The N-th parcel is stored into a file in the current
directory named

```
  FILE-N(-LABEL)-SUFFIX.EXT
```

where SUFFIX and EXT are controlled by command-line arguments and the LABEL part
is optional. The contents and labels of each parcel are determined by the
contents of file.split according to the following syntax.

- `$` indicates the start of a new parcel.

- `${ preamble $}` indicates that "preamble" is to be copied at the beginning of
  each subsequent parcel.

- `$$` indicates the start of a new parcel and marks the rest of the line as a
  comment.

- `$$$word` indicates the start of a new parcel and sets the current label to
  "word".

A known limitation is that it is not currently possible to create a parcel
containing the '$' character.

## run_test utility

Usage: `run_test file.ls` runs a command-line program, typically a compiler, on
file.ls and checks that the results are as expected. The program to run and its
results are specified inside the files using the following syntax.

```
  run_test:
   [ Good: "compiler1"
     Bad n: "compiler2"
     Bad n "regexp": "compiler3"
     Warning: "compiler4"
     Warning "regexp": "compiler5"  ]
```
