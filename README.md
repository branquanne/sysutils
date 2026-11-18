# sysutils

This repository contains three small C/Unix projects:

- [`mdu/`](./mdu/) - disk-usage calculation with optional parallel directory traversal.
- [`mexec/`](./mexec/) - executes commands read from standard input or a file and connects them with pipes.
- [`mmake/`](./mmake/) - a minimal `make`-like build tool based on file modification times.

Each project is built independently from its own directory. The programs use
POSIX APIs such as `fork`, `exec`, `waitpid`, `pipe`, `pthread`, and `stat`, so
they are intended for Unix-like systems.

## Building

Run `make` in the project directory you want to build:

```sh
cd mdu && make
cd ../mexec && make
cd ../mmake && make
```

Use `make clean` in each directory to remove object files and the executable.

## Project relationships

The projects are independent, but they can be used together. For example,
`mmake` can build a project described by a supported makefile, while `mexec`
can run a sequence of shell commands connected by pipes.

## Notes

- Build flags enable GNU C11, warnings, and debug information.
- The implementations are educational and intentionally provide a limited
  subset of the behavior of standard `du`, shell pipelines, and `make`.
- See each subproject README for command-line syntax and input requirements.
