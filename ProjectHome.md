<table><tr><td width='50%' valign='top'>

<h1>!!!Attention!!! New homepage is <a href='http://klish.libcode.org'>http://klish.libcode.org</a></h1>

<h2>About</h2>

The klish is a framework for implementing a CISCO-like CLI on a UNIX systems. It is configurable by XML files. The KLISH stands for Kommand Line Interface Shell. I know that "command" starts with "c" :) .<br>
<br>
The klish is a fork of <a href='clish.md'>clish</a> 0.7.3 project (<a href='http://sourceforge.net/projects/clish/'>http://sourceforge.net/projects/clish/</a>). The original clish was developed by <a href='gmckerrell.md'>Graeme McKerrell</a>. The klish obtain some new features but it's compatible (as much as possible) with clish's XML configuration files. The author of klish project is Serj Kalichev.<br>
<br>
The main target for the klish is a Linux platform. Additionally it can be build on FreeBSD, OpenBSD, Solaris. The QNX support is planned. The klish project is written in C.<br>
<br>
The klish development is sponsored by "Factor-TS" company <a href='http://www.factor-ts.ru/'>http://www.factor-ts.ru/</a>.<br>
<br>
<h2>Repository</h2>

The main klish GIT repository is <a href='https://src.libcode.org/klish'>https://src.libcode.org/klish</a>

<h2>Downloads</h2>

All downloads were moved to <a href='http://klish.libcode.org/files'>http://klish.libcode.org/files</a>
The googlecode.com engine doesn't allow to add new downloads now.<br>
<br>
<h2>Issue tracking</h2>

Post new issues to <a href='http://klish.libcode.org/issues/new'>http://klish.libcode.org/issues/new</a> please.<br>
<br>
<h2>Mailing lists</h2>

The klish related mailing lists:<br>
<ul><li>The klish discussion group <a href='http://groups.google.com/group/klish'>http://groups.google.com/group/klish</a>.<br>
</li><li>The klish development discussion group <a href='http://groups.google.com/group/klish-dev'>http://groups.google.com/group/klish-dev</a>.</li></ul>

</td><td width='50%' valign='top'>
<h2>News</h2>

The klish news blog <a href='http://klish-cli.blogspot.com'>http://klish-cli.blogspot.com</a>.<br>
<br>
<wiki:gadget url="http://google-code-feed-gadget.googlecode.com/svn/build/prod/feedgadget/feedgadget.xml" up_feeds="http://klish-cli.blogspot.com/atom.xml" height="600" width="100%" border="0"/><br>
</td>
</tr>
</table>


---


## Features ##

The klish incorporates all the features of clish. See the clish documentation on http://clish.sourceforge.net for details. Additionally klish has some native features:

  * _[Namespaces or logically nested views](nested_views.md)_. The tag [NAMESPACE](NAMESPACE.md) allows to import the command set from the specified view into another view. So these commands can be used within target view. It allows to create logically nested views. The further view in hierarchy can use commands of previous views. The behaviour is like a CISCO modes (there is the availability to use "configure"-mode commands from "config-if" mode).
  * _[Namespaces with prefix](nested_views.md)_ support. The command set can be included into another view with the prefix. All included commands will obtain specified prefix when used from target view. These feature allow to implement CISCO-like "do show ..." commands.
  * _[Optional arguments](optional_arguments.md)_ support. The command arguments can be optional. The [PARAM](PARAM.md) tag supports "optional" option that specify whether parameter is optional.
  * _[Subcommands](subcommands.md)_ support. The special type of PARAMs was implemented. It's a fixed word (the sequence of symbols with no spaces) that can be found among another arguments. It can be optional and mean a flag.
  * _[Nested parameters](nested_params.md)_ support. The parameters can be nested. The child (nested) parameters follow the parent parameter. This feature use in parameter branching and with optional parameters. If optional parameter is entered then all the child parameters follow. If the optional parameter was not entered than the child parameters will not be used.
  * _[Switch subcommands](switch_subcommand.md)_ support. The special type of subcommand allows to choose one argument of the list of possible arguments as a next positional parameter. So together with the [nested parameters](nested_params.md) it implements the branching. The argument list can be non-linear.
  * _[CISCO-like config](cisco_config.md)_ support. In some cases the CLI is rather useless without configuration commands storing. The new XML tag [CONFIG](CONFIG.md) was implemented to support interaction beetween klish and some external (or internal) mechanism to store some commands sequence i.e. CISCO-like configuration. On each succesfully executed command the klish can execute special callback function that get current command information and can communicate to external tool to store commands or use the internal mechanisms.
  * _[Configuration daemon](konfd.md)_. The configuration daemon [konfd](konfd.md) can store the current CISCO-like configuration information (running-config). Any klish or another process can communicate to [konfd](konfd.md) via socket. There is special string-oriented protocol to set new entries to the running-config, remove existent entries or get current config state.
  * _[The initial view redefinition](CLISH_VIEW.md)_. User can define CLISH\_VIEW environment variable to set initial view instead of the initial view from STARTUP tag.
  * _[The klish specific XML examples](klish_examples.md)_. The klish source tree contain the klish specific XML examples that show basic CISCO-like interface to configure network interfaces and routing in Linux system.
  * _[The ordered sequences](sequence.md)_ support in user configuration. In some cases the ordered numerated lists is needed. The example is a CISCO-like access lists in which the order of entries is important. The entries can be addressed by the line number.
  * _[The automatic internal variables](internal_variables.md)_. For each command the klish engine generates the automatic variables that can be used the same way as a variables origin from PARAM tags. These are current command line (${cmd}), the whole entered line (${line}) etc.
  * _[The klish specific builtin functions](builtin_functions.md)_. The clish contain a set of builtin functions (that don't need a scripting within ACTION tag). The additional klish specific builtin functions is available.
  * _[The conditional parameters](conditional_param.md)_ support. The [parameter](PARAM.md) can be dynamically enabled or disabled depending on the condition. The condition have the syntax same as standard /bin/test utility. So the [parameter](PARAM.md) visibility can depend on the previous [parameters](PARAM.md) values.
  * _[The locking mechanism](locking_mechanism.md)_. The locking mechanism allows to execute several instances of clish utility (or another programs based on libclish library) simultaneously without conflicts.
  * _[The atomic actions](atomic_action.md)_ support. The [ACTION](ACTION.md) script can be non-interruptable for the user. It's a default behaviour.
  * _[The choosing of the scripting language](shebang.md)_ is supported. The scripting language for the [ACTION](ACTION.md) script execution can be customized.
  * _[The command aliases](command_alias.md)_ are supported. The [command](COMMAND.md) can have the aliases. The resulting alias is equal to the original command. To find out what name (original or alias) was used the `${__cmd}` internal variable can be analyzed.
  * _[The buildroot contrib files](buildroot.md)_. The klish source tree contain the contrib files for the [buildroot](http://www.buildroot.net) to be embedded into it as an additional package.
  * _[The UTF-8 encoding support](utf8.md)_. The clish utility can autodetect if current locale use UTF-8 encoding or 8-bit encoding.
  * _[XML backends](xml_backend.md)_. The klish engine supports a several XML backends. That backends parses klish's XML configuration files.
  * _[Programmable hotkeys](hotkeys.md)_. The programmable hotkeys were implemented.

---


## Utilities ##

The utilities reference:

  * [clish](utility_clish.md) - The CLI utility.
  * [konfd](konfd.md) - The daemon to store configuration.
  * [konf](utility_konf.md) - The utility to communicate to konfd daemon from shell.
  * [sigexec](sigexec.md) - The utility to start daemons from non-interruptable ACTION scripts.


---

## XML tags/parameters ##

The following list represents the klish native XML tags of early-known tags with klish native options:

  * [NAMESPACE](NAMESPACE.md)
  * [CONFIG](CONFIG.md)
  * [PARAM](PARAM.md)
  * [VIEW](VIEW.md)
  * [COMMAND](COMMAND.md)
  * [ACTION](ACTION.md)
  * [STARTUP](STARTUP.md)
  * [HOTKEY](HOTKEY.md)


---

## HOWTO ##

See the [HOWTO](HOWTO.md) to find out some klish related questions.


---

(C) _Serj Kalichev <serj.kalichev(`_at_`)gmail.com>, 2010_