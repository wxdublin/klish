

# Introduction #

The original clish contain a set of builtin functions that don't need a scripting within ACTION tag. The example of of using builtin function from original clish. This command closes the current clish session.

```
    <COMMAND name="logout"
             help="Logout of the current CLI session">
        <ACTION builtin="clish_close"/>
    </COMMAND>
```

The additional klish specific builtin functions is available.

# Details #
## clish\_nested\_up ##

The klish supports the [nested\_views](nested_views.md) nested views. When user moves deeper in the [VIEW](VIEW.md)'s hierarchy (the 'depth' of [VIEW](VIEW.md)s is increasing) the engine create entries in the "nesting" stack to save previous [VIEW](VIEW.md) and its state. The clish\_nested\_up function make 'pop' stack operation so it restores previous [VIEW](VIEW.md) and its state. If the current depth is 0 then the clish\_nested\_up function will be an analog of clish\_close builtin function and will close the current klish session.

The feature is available starting with klish-1.2.1.

## clish\_nop ##

The NOP command. It does nothing. It's usefull for commands like comment. The CISCO uses "!" as a comment. If the command has no [ACTION](ACTION.md) tag at all then this command is unfinished so the "Enter" can't be pressed. Use clish\_nop for empty commands. Don't use `<ACTION></ACTION>` because it's slower.

The feature is available starting with klish-1.4.2.