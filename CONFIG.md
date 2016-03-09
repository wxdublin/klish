

# Introduction #

The CONFIG tag was implemented to support interaction beetween klish engine and some external (or internal) mechanism to store a commands sequence i.e. CISCO-like configuration.

# Options #

## `[operation]` ##

Define the action on current configuration (running-config):

  * set - write currently entered command line to the running-config. If the command is already in the running-config it will be no changes. The "pattern" field define the uniqueness of command. If the running-config already contain entries starting with the "pattern" than these entries will be removed.
  * unset - remove entries from the running-config due to specified "pattern".
  * dump - write the running-config to the specified "file". If the "file" is not specified than running-config will be written directly to the communication channel (the socket in the case of "[konfd](konfd.md)" configuration backend). So the config callback function must care about data receiving. The standard callback can receive and show the data from "[konfd](konfd.md)" daemon.

The default is "set".

## `[priority]` ##

The "priority" field define the sort order within running-config. Note the order of commands is important. For example to setup routing table the interfaces must be already configured.

The "priority" is a two-byte hex number (for example "0x2345"). The high byte defines the configuration group of command. The low byte defines the priority within the group. The configuration groups is separated from each other with "!" symbol. The commands within group can be separated or not separated with "!". The separation behaviour within group is defined by "splitter" field. For example the CISCO-like running-config will separate the definitions of interfaces with "!" but will not separate "ip route ..." and "ip default-gateway ..." commands.

The default is "0x7f00". It's a medium value of the high-byte.

## `[pattern]` ##

The field specify the pattern to remove entries from running-config while "unset" operation and the identifier of unique command while "set" operation.

The default is the name of the current command (`${__cmd}`).

## `[file]` ##

This field defines the filename to dump running-config to.

## `[splitter]` ##

A boolean flag. The allowed values is true or false. If the "splitter" is "true" than the current command will be separated with the "!" symbol within its configuration group. See the "priority" description for details about configuration groups.

Default is true.

# Notes #

The CISCO-like config supports nested commands. It uses indention as a syntax for the nesting. To specify nesting depth of command the "depth" option of [VIEW](VIEW.md) tag is used. All the commands of view have the same depth.