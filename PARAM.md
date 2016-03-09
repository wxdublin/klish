

# Introduction #

The PARAM tag defines command parameters. This document describes klish native options only. See the [clish](clish.md) documentation for  the other PARAM options. See the [optional arguments](optional_arguments.md), [subcommands](subcommands.md) and [switch subcommands](switch_subcommand.md) for the information about using new features of PARAM tag.

# Options #

## `[optional]` ##
A boolean flag. Specify whether parameter is optional. The allowed values is true or false.

Default is false.

## `[order]` ##
A boolean flag. Can be used with optional (optional="true") parameters only. If current parameter is specified in command line then previously declared (in XML file) other optional parameters can't be entered later. So this option set the order of available optional parameters. See the [Optional arguments](optional_arguments.md) page for example.

The allowed values is true or false. Default is false.

The feature is available since version 1.5.2 or SVN [revision #522](https://code.google.com/p/klish/source/detail?r=#522).

## `[mode]` ##
Define parameter behaviour. It can be:

  * common - the standard mode for ordinary parameter. Nothing special.
  * subcommand - the parameter is [subcommand](subcommands.md). The subcommand is identified by its "name" (or "value" field if specified) and can be used as optional flag or for the branching. If the subcommand was used then the value of parameter is its name ("value" field if specified). The value of parameter is undefined if parameter is optional and was not used. See the [subcommand](subcommands.md) and "value" field documentation for details.
  * switch - the parameter is [switch subcommand](switch_subcommand.md). The switch subcommand's sub-parameters is alternative and allow branching implementation. The parameter itself get the name of choosen sub-parameter as a value. See the [switch subcommand](switch_subcommand.md) documentation for details.

Default is "common".

## `[value]` ##

The [subcommand](subcommands.md) specific option. This field is used to separate the name of internal variable and the displayable name (that user will enter). The "name" field is a name of the internal variable. The "value" is a displayable subcommand name. It allows to duplicate displayable subcommand names.

The "value" field forces the mode of PARAM to "subcommand".

The feature is available since version 1.2.0.

## `[hidden]` ##

The 'hidden' field specify the visibility of the parameter while [`${\_\_line}`](internal_variables.md) and [`${\_\_params}`](internal_variables.md) automatic variables expanding. The expanding of variable with the PARAM name is performed by the usual way. The allowed values is "true" or "false".

Default is "false".

For example this feature can be used while the [ordered sequences](sequence.md) implementation. The hidden parameter can specify the line number in [ordered sequence](sequence.md). So it must be passed to the [konfd](konfd.md) daemon via [sequence](sequence.md) field of CONFIG tag but the `${__line}` (that will be set to the user config) doesn't need to contain line number.

## `[test]` ##

The parameter can be dynamically enabled or disabled depending on the condition. The condition have the syntax same as standard /bin/test utility. So the parameter visibility can depend on the previous parameters values and [internal variables](internal_variables.md). See the [conditional parameters](conditional_param.md) for details.

By default the parameter is enabled.