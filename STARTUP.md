

# Introduction #

The STARTUP tag defines the starting view, viewid and the other startup settings. This document describes klish native options only. See the [clish](clish.md) documentation for the other STARTUP options.

# Options #

## `[default_shebang]` ##

Defines the scripting language (the binary file) to use for the [ACTION](ACTION.md) script execution by default.

Default is the "/bin/sh". The [ACTION](ACTION.md) tag with 'shebang' field can locally redefine the shebang for its execution.

## `[timeout]` ##

Without any user activity for the specified timeout the klish can autologout (close current input stream and exit). It can be used to automatically close privileged sessions when the administrator have forgot to close session manually.

## `[lock]` ##

The same as "lock" field of [COMMAND](COMMAND.md) tag.

## `[interrupt]` ##

The same as "interrupt" field of [COMMAND](COMMAND.md) tag.