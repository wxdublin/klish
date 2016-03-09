

# Introduction #

The COMMAND tag defines the command. This document describes klish native options only. See the [clish](clish.md) documentation for  the other COMMAND options. See the [locking mechanism](locking_mechanism.md) for the information about using new features of COMMAND tag.

# Options #

## `[lock]` ##
A boolean flag. It can enable (true) or disable (false) the [locking mechanism](locking_mechanism.md) for the current command.

Default is true.

## `[ref]` ##
The 'ref' field is used to create a [command alias](command_alias.md). If the 'ref' field is used within COMMAND definition that command is not standalone but it's an [alias](command_alias.md). The 'ref' contain the name of target original command to make alias of. In the case if the target command belongs to the another view than the view of alias then the target command's view must be specified after the target command name. The delimeter beetween the command name and view name is "@" symbol. See the [command alias](command_alias.md) page for the details and examples.

## `[interrupt]` ##
The 'interrupt' field specifies if the [ACTION](ACTION.md) script is interruptable or non-interruptable by the user. If the interrupt="true" than the script is interruptable else the script is non-interruptable. For non-interruptable scripts the SIGINT and SIGQUIT is temporarily blocked. See the [atomic actions](atomic_action.md) for the details. The 'interrupt' field is available since SVN [revision 347](https://code.google.com/p/klish/source/detail?r=347) or klish-1.4.0.