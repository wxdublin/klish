

# Introduction #

The [command](COMMAND.md) can have the aliases. The resulting alias is equal to the original command except the name of command, help text and the value of internal variable `${__cmd}`.

# Details #

To find out what name (original or alias) was typed by the user the `${__cmd}` internal variable can be analyzed. The `${__orig_cmd}` variable contain the name of the original command (the target of alias). See [internal variables](internal_variables.md) page for details about internal variables. The `${__cmd}` can be analyzed within [ACTION](ACTION.md) and within ['test' field](conditional_param.md) of [PARAM](PARAM.md) tag.

The 'ref' field of [COMMAND](COMMAND.md) tag is used to create alias of command. The following example creates the alias (named "info") for the original command "show running-config" from the view "view1":

```
<COMMAND name="info" ref="show running-config@view1" help="Alias for the show running-config command"/>
```

The following example creates alias (named "conf") for the command "info" from the current view (the view of both "conf" and "info" commands):

```
<COMMAND name="conf" ref="info" help="Alias for the info command"/>
```