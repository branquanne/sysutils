# mexec

`mexec` is a small pipeline executor. It reads one command per line, starts
each command in a child process, and connects consecutive commands with Unix
pipes.

## Build

```sh
make
```

This produces the `mexec` executable. Remove build artifacts with:

```sh
make clean
```

## Usage

Read commands from standard input:

```sh
./mexec
```

Read commands from a file:

```sh
./mexec commands.txt
```

Each non-empty line is split on spaces, tabs, and newlines. For example,
`commands.txt` could contain:

```text
cat input.txt
grep error
wc -l
```

The commands are executed as a pipeline equivalent to:

```sh
cat input.txt | grep error | wc -l
```

Commands are resolved with `execvp`, so executable names are searched using the
current `PATH`. The input format does not provide shell parsing: quoting,
variable expansion, redirection, and shell operators are not interpreted.

The process exits unsuccessfully if parsing, process creation, execution, or a
child command fails. The optional `mmakefile` in this directory is an input
makefile, not the build file used by the repository's `make` command.
