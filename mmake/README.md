# mmake

`mmake` is a minimal `make`-like build utility. It reads rules from a
makefile, recursively builds prerequisites, and runs a target's command when
the target is missing or older than one of its prerequisites.

## Build

```sh
make
```

This produces the `mmake` executable. Remove build artifacts with:

```sh
make clean
```

## Usage

```text
./mmake [-f MAKEFILE] [-B] [-s] [TARGET ...]
```

- `-f MAKEFILE` reads rules from an alternative file. The default is
  `mmakefile`.
- `-B` forces targets to be rebuilt.
- `-s` suppresses printing commands before they are executed.
- If no target is supplied, the first rule is used.

Example:

```sh
./mmake
./mmake clean
./mmake -B mmake
./mmake -f custom.mk all
```

## Makefile format

Rules use one target line followed by one tab-indented command line:

```make
program: main.o
	gcc -o program main.o

main.o: main.c
	gcc -c main.c -o main.o
```

Prerequisites are built recursively. Commands are executed directly with
`execvp`; shell syntax such as pipes, redirection, and wildcard expansion is
not interpreted. The parser supports a deliberately small makefile format,
with bounded line, prerequisite, and command sizes.
