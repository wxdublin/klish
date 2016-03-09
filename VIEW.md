

# Introduction #

The VIEW tag defines a view. The view aggregates the commands.

# Options #

## `[depth]` ##
A depth of nested view. It is used together with the [CONFIG](CONFIG.md) tag. If the command must be written to the config the view's depth specifies the command indention within [CISCO-like config](cisco_config.md). All the commands within current VIEW have the same depth.

The default is "0".

## `[restore]` ##
The commands contained by the view can be executed from the nested views or parallel views using the [NAMESPACE](NAMESPACE.md). While the command execution the depth (and a context) or the view of command can be restored. The value of 'restore' field can be:

  * none - Don't change the current view.
  * view - The current view will be set to the command's native view.
  * depth - The klish engine will find out the depth of command's native view. Then it will search for this depth in the current nested views stack. The current view will be set to the saved view from the stack with the depth equal to command's depth. Additionally the context (the viewid) will be restored from the stack.

Default is "none". See the [nested views](nested_views.md) wiki page for the additional information and example.