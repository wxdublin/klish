

# Introduction #

The command arguments can be optional. The [PARAM](PARAM.md) tag supports "optional" parameter that specify whether parameter is optional. It can be a sequence of optional parameters. The order of optional parameters define the order to validate values. If the value was succesfully validated by optional parameter the next optional parameters will not validate this value. Each parameter can be specified only once. See the [PARAM](PARAM.md) for the tag description.

# Details #

The following code creates three optional arguments and the mandatory one:

```
        <PTYPE name="SUBCOMMAND"
                pattern="[^\]+"
                help="String"/>

        <COMMAND name="com2" help="Command 2">

                <PARAM name="flag"
                        help="option -c"
                        ptype="SUBCOMMAND"
                        mode="subcommand"
                        optional="true"/>

                <PARAM name="-c"
                        help="option -c"
                        ptype="SUBCOMMAND"
                        mode="subcommand"
                        optional="true"/>

                <PARAM name="p_int"
                        help="optional uint param"
                        ptype="UINT"
                        optional="true"/>

                <PARAM name="mandatory"
                        help="mandatory uint param"
                        ptype="SUBCOMMAND"
                        mode="subcommand"/>

                <ACTION>
                if test "x${flag}" != "x"; then echo "flag=${flag}"; fi
                if test "x${-c}" != "x"; then echo "-c=${-c}"; fi
                if test "x${p_int}" != "x"; then echo "p_int=${p_int}"; fi
                echo "${mandatory}"
                </ACTION>
        </COMMAND>
```

If optional parameters has not been entered then corresponding variable will not be set. The optional parameters can be used in arbitrary order.

# Ordered optional parameters #

In previous example all three optional parameters can be used in arbitrary order i.e. you can enter the "-c" parameter first and "flag" parameter later or any other order. The "order" field of [PARAM](PARAM.md) tag makes the sequence of optional parameters ordered.

```
                 <PARAM name="flag"
                        help="option -c"
                        ptype="SUBCOMMAND"
                        mode="subcommand"
                        optional="true"/>

                <PARAM name="-c"
                        help="option -c"
                        ptype="SUBCOMMAND"
                        mode="subcommand"
                        optional="true"
                        order="true"/>

                <PARAM name="p_int"
                        help="optional uint param"
                        ptype="UINT"
                        optional="true"/>
```

Notice the order="true" field within "-c" subcommand definition. Now the "flag" optional parameter can't be entered if "-c" is already entered. So the parameter with order field cut off all previously declared optional parameters.

# The clish compatibility #

The [clish](clish.md) has the optional parameters support too but there is a differencies. The "prefix" [PARAM](PARAM.md) option definition means that parameter is optional and the prefix must be followed by argument with "ptype" specified in the same [PARAM](PARAM.md). So the parameter without prefix cannot be optional.

The klish emulates clish behaviour when the "prefix" option is defined. The following two [PARAM](PARAM.md)s is equivalent.

  * The klish native variant:
```
                <PARAM name="-c"
                        help="option -c"
                        ptype="SUBCOMMAND"
                        mode="subcommand"
                        optional="true">

                        <PARAM name="p_int"
                                help="optional uint param"
                                ptype="UINT"/>

                </PARAM>
```

  * The clish compatible variant:
```
                <PARAM name="p_int"
                        help="optional uint param"
                        ptype="UINT"
                        prefix="-c"/>
```

The internal representation of these parameters is the same. The klish native variant can show the internal representation. It use [nested parameters](nested_params.md) mechanism. Actually the clish variant use internal ptype "internal\_SUBCOMMAND" for auto-generated optional subcommand named "-c". It cannot use "SUBCOMMAND" ptype bacause it can be undefined. The "internal\_SUBCOMMAND" ptype has pattern="`[^\]+`" and help="Option".

The clish variant seems to be shorter but it doesn't work if you need several sub-parameters or if you don't need any sub-parameters at all but only the flag.