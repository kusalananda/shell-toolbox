# shell-toolbox
Useful shell scripts and functions, mostly for `ksh93` and `bash`.

The scripts and functions are documented in the source.


## Shell functions (in `fun/`)

* `shell`:  _Creates a shell for testing things in_.  Creates a
temporary shell with a temporary working directory.  The working
directory is removed when the shell exits.  Useful for testing things
in an interactive environment other than your usual shell.  Works with
`ksh93` and
`bash`.

* `shtest`: _Runs a command in all shells_.  Iterates over all installed
shells and runs the same command in all of them, capturing and
displaying the exit status and the output sent to all standard streams.
Useful for testing compatibility of shell constructs between shells.
Works with `ksh93` and `bash`.
