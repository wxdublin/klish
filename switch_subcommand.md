

# Introduction #

The special type of [PARAM](PARAM.md) was implemented. The switch subcommand is a container that allow to choose the only one of its sub-parameters for further analyzing.

# Details #

The following example shows the command with switch subcommand:

```
        <COMMAND name="com" help="Command">

                <PARAM name="choice"
                        help="Switch subcommand"
                        ptype="STRING"
                        mode="switch">

                        <PARAM name="one"
                                help="one subcommand"
                                ptype="SUBCOMMAND"
                                mode="subcommand"/>

                        <PARAM name="two"
                                help="two subcommand"
                                ptype="SUBCOMMAND"
                                mode="subcommand">

                                <PARAM name="nint"
                                        help="nested int"
                                        ptype="UINT"/>

                        </PARAM>

                </PARAM>

                <PARAM name="mandatory"
                        help="mandatory uint param"
                        ptype="UINT"/>

                <ACTION>
                echo "Choice is ${choice}"
                echo "one is ${one}"
                echo "two is ${two}"
                echo "nint is ${nint}"
                </ACTION>

        </COMMAND>
```

To define the switch subcommand the [PARAM](PARAM.md)'s option "mode" must be set to "switch". The "ptype" of switch subcommand define PTYPE for sub-parameters names validation.

When the user types "com" he must choose the one of two variants: "one" or "two". So user choose the branch for futher command line parsing. The switch subcommand named "choice" will be set to the name of choosen sub-parameter so you can analyze this value later. The variable with name of choosen sub-parameter will be set to its own name. The variables with names of sub-parameters that were not choosen will be unset.

Suppose we choose the "two" sub-parameter. This [subcommand](subcommands.md) contain [nested parameter](nested_params.md) named "nint". The next command line argument will parsed for the "nint" parameter. Then the engine will return to the normal flow and will analyze "mandatory" parameter. The "one" variable will be unset and the "choice" value will be "two". So it implements branching. The "one" branch was not used at all.
