

# Introduction #

For each command the klish engine generates the automatic variables that can be used the same way as a variables origin from [PARAM](PARAM.md) tags. To specify these variables use ${`<name>`} syntax. The variables will be expanded before execution of ACTION, before using some tag's fields that is dynamic and allow the using of variables. The example of such field is [CONFIG](CONFIG.md)'s 'pattern'.

# The automatic internal variables #

## `${__cmd}` ##

The `${__cmd}` contain the name of the current command.

## `${__orig_cmd}` ##

The `${__orig_cmd}` contain the name of the original command if the current command is [alias](command_alias.md). If the current command is not [alias](command_alias.md) the `${__orig_cmd}` is equal to the `${__cmd}`.

## `${__full_cmd}` ##

The `${__full_cmd}` is the entered name of command. When the using of command is simple the `${__full_cmd}` will be equal to `${__cmd}` variable. But when the command was imported from another [VIEW](VIEW.md) using the [NAMESPACE](NAMESPACE.md) tag with specified 'prefix' field, the `${__full_cmd}` will contain the full name of command "`<prefix>` `<command>`".

For example the "show" command is defined in the [VIEW](VIEW.md) "enable-view". The current [VIEW](VIEW.md) is "configure-view". The [VIEW](VIEW.md) "enable-view" is imported into "configure-view" using [NAMESPACE](NAMESPACE.md) tag with field prefix="do". If user enters "do show" in command line than the `${__cmd}`="show" but `${__full_cmd}`="do show".

## `${__params}` ##

The `${__params}` contain all the entered command parameters. It's equal to line entered by user without command name. If one of the parameters contain spaces than this parameter will be quoted within `${__params}` line.

## `${__line}` ##

The `${__line}` is equal to "`${__cmd}` `${__params}`".

## `${__full_line}` ##

The `${__full_line}` is equal to "`${__full_cmd}` `${__params}`".

## `${__prefix}` ##

If the current command is imported from another [VIEW](VIEW.md) using [NAMESPACE](NAMESPACE.md) tag with specified prefix than the `${__prefix}` will contain the actually entered prefix (the prefix definition can be a regexp).

## `${__prefix<num>}` ##

If the current command has several prefixes in a case of nested imports than the `${__prefix<num>}` will contain the actually entered prefix with number `<num>` in a line. The `${__prefix0}` is equal to `${__prefix}`.

## `${__cur_depth}` ##

The `${__cur_depth}` contain the current depth of [nested views](nested_views.md). Note it's not a depth of current command's [VIEW](VIEW.md) but a depth of current [VIEW](VIEW.md). These values is not equal when the command is imported from the another [VIEW](VIEW.md).

## `${__cur_pwd}` ##

The `${__cur_pwd}` contain the "path" to the current [VIEW](VIEW.md). The views can be [nested](nested_views.md) and the commands that lead to changing view to the current [VIEW](VIEW.md) is the current "path". These commands is quoted and delimeted by the space. Usually the "path" is used while communication to the [konfd](konfd.md) daemon. It allows to find out the position and depth of current command in the user config.

## `${__interactive}` ##

The `${__interactive}` can be used to find out if the [clish](utility_clish.md) session is interactive (`${__interactive}` is equal to "1") or non-interactive (`${__interactive}` is equal to "0"). By default the session is interactive. But the [clish utility](utility_clish.md) can be executed with the "--background" option to make session non-interactive.

## `${__isatty}` ##
The `${__isatty}` variable indicates if command was entered manually (using interactive tty) or it come from file or piped stdin. The value will be equal to "1" if command was entered manually and user have interactive tty. The value will be equal to "0" if command came from file.

The variable is available since SVN [revision #546](https://code.google.com/p/klish/source/detail?r=#546) or klish-1.5.2 release.


## `${__width}` ##

The current terminal width (columns).

## `${__height}` ##

The current terminal height (rows).

## `${__watchdog_timeout}` ##

The current watchdog timeout. When the watchdog is inactive the value is "0".

## `${__pid}` ##
The `${__pid}` variable contain the PID of current klish instance (process). It can be useful for storing some session specific data. Note the several klish instances can be executed concurrently.

The variable is available since klish-1.6.9 and klish-1.7.0 releases.

# The automatic variables using example #

The example shows the using of automatic internal variable `${__line}` in CONFIG's pattern field.

```
        <COMMAND name="interface ethernet"
                help="Ethernet IEEE 802.3"
                view="configure-if-view"
                viewid="iface=eth${iface_num}">
                <PARAM name="iface_num"
                        help="Ethernet interface number"
                        ptype="IFACE_NUM"/>
                <CONFIG priority="0x2001" pattern="^${__line}$"/>
        </COMMAND>
```