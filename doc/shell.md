SHELL(1) - General Commands Manual

# NAME

**shell** - Creates a temporary interactive shell session in a disposable working directory

# SYNOPSIS

**shell**
\[**-f**]
\[**-q**]
\[**-d**&nbsp;*directory*&nbsp;|&nbsp;**-k**]
\[*shell*&nbsp;\[*...*]]  
**shell**
\[**-f**]
\[**-q**]
\[**-s**&nbsp;*directory*]
\[**-k**]
\[*shell*&nbsp;\[*...*]]  
**shell**
**-v**

# DESCRIPTION

The
**shell**
utility creates an interactive shell session with a clean environment
and with an empty working directory.

By specifying a specific
*shell*
on the command line, a shell other than the user's login shell may be
invoked.
If a specific shell is not requested, the
`SHELL`
environment variable will be used to infer what shell to start.

The basename of the named
*shell*
must correspond to a valid login shell and the actual shell that is
started will always be taken from the list of valid login shells (by
matching the basename of the specified
*shell*,
or
`$SHELL`,
against the basenames of
the allowed login shells).
This behaviour may be bypassed by using the
**-f**
command line option.

Any operands present after the name of the
*shell*
will be passed as is to the shell in question.

If
**shell**
(this utility,
*not*
the interactive shell process) receives the USR1 signal, the temporary
working directory will not be deleted when the shell session terminates
(as if
**-k**
had been used from the start).

The options are as follows:

**-d** *directory*

> Use the specified directory rather than a new temporary directory.
> If the directory does not already exist, it will be created.
> This directory will not be deleted when the shell session terminates.
> This option implies the
> **-k**
> option, and conflicts with the
> **-s**
> option.

**-f**

> Force the execution of the given command, even if it is not a valid
> login shell on the current system.

**-k**

> Keep the temporary directory around after terminating the shell session.

**-q**

> Be quiet.
> Don't output informational messages.

**-s** *directory*

> Pre-populate the temporary directory with the contents of the named
> directory.
> This will copy the whole directory structure rooted in the specified
> directory to the temporary working directory.
> This option conflicts with the
> **-d**
> option.

**-v**

> Output version information and immediately terminate.

# ENVIRONMENT

**shell**
uses the following environment variables:

`SHELL`

> Used to determine what shell to start if a specific
> *shell*
> is not specified on the command line.
> If this variable is unset or empty, then
> **/bin/sh**
> will be used instead.

`SHELL_SKEL`

> Directory to automatically pre-populate the temporary working directory with.
> This environment variable is not used if any of the
> **-d**
> or
> **-s**
> options are used on the command line.

`TMPDIR`

> Directory in which to create the working directory when the
> **-d**
> option is not used.
> This variable is used by
> **mktemp**
> which will revert to use
> */tmp*
> if the variable is not set.

**shell**
clears the environment of the interactive shell that it starts, but
also sets the following environment variables:

`HOME`

> Set to the working directory where the shell is started.

`PATH`

> Set to the output of
> "**getconf PATH**".

`PS1`

> Set to the string
> '$&#160;'
> (dollar-sign and space).
> Note that some shells ignore this variable if passed from the parent
> environment.

`SHELL`

> Set to the absolute path of the real shell executable.
> This may be different from the
> *shell*
> mentioned on the command line as the actual shell used will be picked
> from the list of valid login shells (unless
> **-f**
> is used).

`TERM`

> Carried over from the parent environment.

# FILES

*/etc/shells*

> Used as a source for valid login shells on systems where
> "**getent shells**"
> does not work.

# EXAMPLES

Start a new shell in a new temporary directory:

	$ shell
	shell: info: Starting /bin/ksh in /tmp/shell-ksh.mJMHFTFE
	$ exit
	shell: info: Removing /tmp/shell-ksh.mJMHFTFE

Start a new
**dash**
shell in a temporary directory:

	$ shell dash
	shell: info: Starting /usr/local/bin/dash in /tmp/shell-dash.V7zU6EtZ
	$ exit
	shell: info: Removing /tmp/shell-dash.V7zU6EtZ

Start a new
**bash**
shell in a specific directory:

	$ shell -d "$HOME/testing" bash
	shell: info: Starting /usr/local/bin/bash in /home/myself/testing
	$ exit
	exit
	shell: info: Leaving /home/myself/testing in place

Start
**ksh**
as a login shell and pre-populate the temporary directory with the
contents of
*$HOME/skel*.
Note, starting the
**ksh**
shell as a login shell will in this case make it execute the
*.profile*
file copied from
*$HOME/skel*.

	$ shell -s "$HOME/skel" ksh -l
	shell: info: Copying /home/myself/skel into /tmp/shell-ksh.ngEwbcpD
	shell: info: Starting /bin/ksh in /tmp/shell-ksh.ngEwbcpD
	$ ls -la
	total 36
	drwxr-xr-x   2 myself  wheel  512 Apr 15 12:55 .
	drwxrwxrwt  28 root    wheel  512 Apr 21 14:15 ..
	-rw-r--r--   1 myself  wheel   87 Nov  1 19:14 .Xdefaults
	-rw-r--r--   1 myself  wheel  771 Feb  9 10:18 .cshrc
	-rw-r--r--   1 myself  wheel  101 Nov  1 19:14 .cvsrc
	-rw-r--r--   1 myself  wheel  359 Nov  1 19:14 .login
	-rw-r--r--   1 myself  wheel  175 Nov  1 19:14 .mailrc
	-rw-r--r--   1 myself  wheel  215 Feb  9 10:18 .profile
	-rw-r--r--   1 myself  wheel  108 Apr 15 12:50 .vimrc
	$ exit
	shell: info: Removing /tmp/shell-ksh.ngEwbcpD

# SEE ALSO

mktemp(1)

# AUTHORS

Andreas Kusalananda K&#228;h&#228;ri &lt;[andreas.kahari@nbis.se](mailto:andreas.kahari@nbis.se)&gt;

# CAVEATS

For Solaris, the list of valid login shells is taken from the
shells(4)
manual on a vanilla Solaris 11.4 system.
This is because Solaris lacks
"**getent shells**"
and may also lack the
*/etc/shells*
file.
The
*/etc/shells*
file will still be used if it exists.

Unix - July 19, 2018
