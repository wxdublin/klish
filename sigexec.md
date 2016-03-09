

# Synopsis #

**`sigexec [options] <command to execute>`**

# Description #

The sigexec utility unblocks (by sigprocmask()) all signals and executes specified command. It's usefull within [non-interruptable](atomic_action.md) [ACTION](ACTION.md) scripts for daemon starting. The daemon will have clean signal mask.

# Options #

## `-v, --version` ##
Print the version of utility.

## `-h, --help` ##
Print help.