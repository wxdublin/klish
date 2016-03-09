

# Introduction #

The HOTKEY tag allows to implement programmable hotkeys. The global view (XML configuration without explicit view definition) and [VIEW](VIEW.md)s can contain HOTKEY tags. See [hotkeys](hotkeys.md) page for additional information.

The HOTKEY tag was implemented since klish-1.5.7 and klish-1.6.2.

# Options #

## `[key]` ##
The symbolic key description. The klish supports control keys with "Ctrl" ("`^`" symbol) only. Some combination are internally reserved (like a Ctrl`^`C and some other keys). To define a key use "`^[key_simbol]`". For example:
```
<HOTKEY key="^Z" .../>
<HOTKEY key="^S" .../>
```
The first line is for `Ctrl^Z` and the second is for `Ctrl^S` combinations accordingly.

## `[cmd]` ##
The klish [COMMAND](COMMAND.md) with arguments to execute on specified hotkey combination. This command must be defined in XML config. The command string can contain dynamically expanded [VAR](VAR.md)s.

```
<HOTKEY key="^Z" cmd="exit"/>
<HOTKEY key="^@" cmd="show running-config"/>
<HOTKEY key="^S" cmd="echo ${HOSTNAME}"/>
<VAR name="HOSTNAME" ... />
```