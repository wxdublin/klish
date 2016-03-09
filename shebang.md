

# Introduction #

The scripting language for the [ACTION](ACTION.md) script execution can be customized. Additionally the user can define the default scripting language for the whole session.

# Details #

The [shebang](http://en.wikipedia.org/wiki/Shebang_%28Unix%29) can be specified for the [ACTION](ACTION.md) script execution. By default the "/bin/sh" is used. To customize shebang the 'shebang' field of the [ACTION](ACTION.md) tag is used:

```
<COMMAND ...>
        ...
        <ACTION shebang="/usr/bin/perl -w">
                print "Hello world\n";
        </ACTION>
</COMMAND>
```

To define the default shebang for the whole session the 'default\_shebang' field of the [STARTUP](STARTUP.md) tag is used:

```
<STARTUP default_shebang="/bin/bash" ... />
```