

# Introduction #

The NAMESPACE tag allows to import the command set from the specified view into another view. See the [logically nested views](nested_views.md) for details on using this tag.

# Options #

## ref ##
Reference to the view to import commands from.

## `[prefix]` ##
The prefix for imported commands.

## `[inherit]` ##
A boolean flag whether to inherit nested namespace commands recursively. Can be true or false. Default is true.

## `[help]` ##
A boolean flag whether to use imported commands while help. Can be true or false. Default is false.

## `[completion]` ##
A boolean flag whether to use imported commands while command completion. Can be true or false. Default is true.

## `[context_help]` ##
A boolean flag whether to use imported commands while context help. Can be true or false. Default is false.