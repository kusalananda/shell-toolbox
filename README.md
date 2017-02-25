# shell-toolbox
Useful shell scripts and functions, mostly for ksh93 and bash.

The scripts and functions are documented in the source.


## Shell functions (`fun/`)

* `shell`:  _Creates a shell for testing things in_.
Creates a temporary shell with a temporary working directory.  Tho
working directory is removed when the shell exits.

* `shtest`: _Runs a command in all shells_.
Iterates over all installed shells and runs the same command in all of
them, capturing and displaying the exit status and the output sent to
all standard streams.
