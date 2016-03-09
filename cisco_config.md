

# Introduction #

In some cases the CLI is rather useless without configuration commands storing. The new XML tag [CONFIG](CONFIG.md)  was implemented to support interaction beetween klish and some external (or internal) mechanism to store some commands sequence i.e. CISCO-like configuration. On each succesfully executed command the klish can execute special callback function that get current command information and can communicate to external tool to store commands or the internal mechanisms can be used for config storing.

The default tool to store configuration is [konfd](konfd.md) daemon accessible over socket interface.

# Details #

The [CONFIG](CONFIG.md) tag is used to make klish to store the current command or execute other actions (remove old entries, dump entries to file) on config. See [CONFIG](CONFIG.md) page for details about tag syntax.