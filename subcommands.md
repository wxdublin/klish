

# Introduction #

The special type of [PARAM](PARAM.md) was implemented. It's a fixed word (the sequence of symbols with no spaces) that can be found among another arguments. The subcommand is identified by its name (or "value" field if specified) and can be used as optional flag or for the branching. If the subcommand was used then the value of parameter is its name ("value" field if specified). The value of parameter is undefined if parameter is optional and was not used. See the [PARAM](PARAM.md) for the tag description.

# Details #

The following example shows typical subcommand definition.

```
        <PTYPE name="SUBCOMMAND"
                pattern="[^\]+"
                help="String"/>

        <PARAM name="-c"
                help="option"
                ptype="SUBCOMMAND"
                mode="subcommand"
                optional="true"/>
```

The [PARAM](PARAM.md) tag contain "mode" option. This option must be "subcommand" for subcommands. See the "mode" option description in [PARAM](PARAM.md). The "ptype" may be arbitrary. The engine will validate the name of [PARAM](PARAM.md) using specified "ptype".

I think there is no reason to use subcommands without optional="true" or without [branching](switch_subcommand.md). See the [optional arguments](optional_arguments.md) and [switch subcommands](switch_subcommand.md) for additional information.

# Subcommand duplication #

The displayable subcommand name can be duplicated by the "value" field. For example the user can use two subcommands "host":

```
               <PARAM name="host1"
                       value="host"
                       help="src host"
                       ptype="SUBCOMMAND"
                       mode="subcommand">
                       <PARAM name="ip_src"
                               help="src host ip"
                               ptype="IP_ADDR"/>
               </PARAM>

               <PARAM name="host2"
                       value="host"
                       help="dst host"
                       ptype="SUBCOMMAND">
                       <PARAM name="ip_dst"
                               help="dst host ip"
                               ptype="IP_ADDR"/>
               </PARAM>
```

The internal [PARAM](PARAM.md)'s variable names will be "host1" and "host2" but the displayable names is "host" for the both parameters. The "value" field forces the mode of [PARAM](PARAM.md) to "subcommand". It have no meaning for another modes. If the "value" field is not specified the internal variable name and displayable name is the same and the "name" field is used.

The feature is available since version 1.2.0.