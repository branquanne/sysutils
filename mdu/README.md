# mdu

`mdu` calculates disk usage for files and directories. Results are reported in
512-byte blocks, matching the value returned by the filesystem's `st_blocks`
field. Directories are traversed recursively.

## Build

```sh
make
```

This produces the `mdu` executable. Remove build artifacts with:

```sh
make clean
```

## Usage

```text
./mdu [-j number_of_threads] file ...
```

Examples:

```sh
./mdu README.md
./mdu src/
./mdu -j 4 src/ include/
```

Without `-j`, traversal is single-threaded. With `-j N` where `N` is greater
than one, paths are processed by `N` worker threads using a shared work queue.
Each output line has the form:

```text
blocks<TAB>path
```

Access errors are reported to standard error, and the program exits
unsuccessfully if any requested path could not be fully accessed.

## Benchmark script

`script.sh` runs the executable for thread counts from 1 through 100 and
writes elapsed times to `performance_results.txt`. It currently benchmarks
`/pkg/`, so edit the `DIRECTORY` variable before using it on another system:

```sh
./script.sh
```

The implementation counts allocated filesystem blocks (`st_blocks`), not
logical file sizes (`st_size`), and does not follow symbolic links.
