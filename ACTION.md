

# Introduction #

The ACTION tag defines the script to execute. This document describes klish native options only. See the clish documentation for the other ACTION options.

# Options #

## `[shebang]` ##

Defines the scripting language (the binary file) to use for the ACTION script execution.

Default is the shebang defined within [STARTUP](STARTUP.md) tag using 'default\_shebang' field. If the 'default\_sheband' is undefined the "/bin/sh" is used.