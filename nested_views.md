

# Introduction #

The tag [NAMESPACE](NAMESPACE.md)  allows to import the command set from the specified view into another view. So these commands can be used within target view. It allows to create logically nested views. The further view in hierarchy can use commands of previous views. The behaviour is like a CISCO modes (there is the availability to use "configure"-mode commands from "config-if" mode). See the [NAMESPACE](NAMESPACE.md) for the tag description.

# Logically nested views #

The following code demonstrates the using of command set import. Assume the current view is "view2". The command "com1" will be available although it belogs to "view1". Additionally the help and completion for commands from "view1" is enabled while import.

```
<VIEW name="view1" prompt="(view1)# ">

        <COMMAND name="com1" help="Command 1">
                <ACTION>echo "com1"</ACTION>
        </COMMAND>

</VIEW>


<VIEW name="view2" prompt="(view2)# ">

        <NAMESPACE ref="view1"
                help="true"
                completion="true"/>

        <COMMAND name="com2" help="Command 2">
                <ACTION>echo "com2"</ACTION>
        </COMMAND>

        <COMMAND name="exit" help="Exit">
                <ACTION builtin="clish_close"/>
        </COMMAND>

</VIEW>
```

# Namespaces with prefix #

The following code do the same thing as a previous example but the commands from "view1" is available with **prefix** "do". Note the new command within "view2" named "do". This command is necessary for klish to resolve any command with this prefix.

```
<VIEW name="view1" prompt="(view1)# ">

        <COMMAND name="com1" help="Command 1">
                <ACTION>echo "com1"</ACTION>
        </COMMAND>

</VIEW>


<VIEW name="view2" prompt="(view2)# ">

        <NAMESPACE ref="view1"
                prefix="do"
                help="true"
                completion="true"/>

        <COMMAND name="do" help="Import prefix"/>

        <COMMAND name="com2" help="Command 2">
                <ACTION>echo "com2"</ACTION>
        </COMMAND>

        <COMMAND name="exit" help="Exit">
                <ACTION builtin="clish_close"/>
        </COMMAND>

</VIEW>
```

# Restore the command context #

When the hierarchy of nested [views](VIEW.md) is built the lower views inherit the [commands](COMMAND.md) from the higher [views](VIEW.md) often. It's true for the CISCO-like configuration mode. See the [klish XML examples](klish_examples.md) in the source tree. For example if the current view is the "configure-if-view" (the nested view to define network interface settings) it's not necessary to obviously "exit" from the current view to the higher level view ("configure-view") to use commands from this higher level view. You can execute these commands directly if the same commands was not redefined in the current view. This feature is used to process the plain [config](cisco_config.md) files.

By default the current view will not be changed. It's good for the information commands like the "do show running-config" that will not get to the [user config](cisco_config.md). But it's not good for the configuration commands. The such commands use the current context (the view, depth and viewid) while execution. So it's necessary to set the command's native context before its execution. The direct call of the higher level command is equal to "exit" from the nested view to the higher level view and then the execution of the specified command. To implement such behaviour without obvious "exit" the 'restore' field of the [VIEW](VIEW.md) tag can be used.

All the commands of the [VIEW](VIEW.md) with specified 'restore' field will restore its context when executed from another view which use [NAMESPACE](NAMESPACE.md) mechanism. See the [VIEW](VIEW.md) tag description for the details. The command can restore only its native view (set it as the current view) if the restore="view" but it's not usefull often. Because this method can't restore viewid and the "configure-view" can include (using [NAMESPACE](NAMESPACE.md)) commands from the other [VIEW](VIEW.md)s with the same depth. The more usefull method for the hierarchy of the nested views is restore="depth". The klish engine will find out the depth of command's native view. Then it will search for this depth in the current nested views stack. The current view will be set to the saved view from the stack with the depth equal to command's depth. Additionally the saved context (the viewid) will be restored from the stack.

The typical "configure-view" has the restore="depth" field:

```
<VIEW name="configure-view"
        prompt="${SYSTEM_NAME}(config)# "
        restore="depth">

    ....

        <COMMAND name="interface"
                help="Select an interface to configure"/>

        <COMMAND name="interface ethernet"
                help="Ethernet IEEE 802.3"
                view="configure-if-view"
                viewid="iface=eth${iface_num}">
                <PARAM name="iface_num"
                        help="Ethernet interface number"
                        ptype="IFACE_NUM"/>
                <CONFIG priority="0x2001" pattern="^${__line}$"/>
        </COMMAND>

    ....

</VIEW>

<VIEW name="configure-if-view"
        prompt="${SYSTEM_NAME}(config-if-${iface})# "
        depth="1">

...

</VIEW>
```