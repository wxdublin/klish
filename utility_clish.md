

# Synopsis #

**`clish [options] [script_filename] [script_filename] ...`**

# Description #

This clish is command line interface shell. The available shell commands and its actions are defined by XML configuration files. The clish utility can get input commands from terminal in interactive mode, from files specified in command line (multiply "script\_filename" arguments) or standard input.

# Options #

## `-v, --version` ##
Print the version of clish utility.

## `-h, --help` ##
Print help.

## `-s <path>, --socket=<path>` ##
The clish utility can work together with the [konfd](konfd.md) daemon. This daemon can store commands entered in clish. It's usefull to implement config file like CISCO's running-config that stores current system configuration i.e. sequence of commands to achieve current system state. The command sequence can be saved to file (CISCO's startup-config) and executed in batch mode later by clish utility.

The [konfd](konfd.md) daemon listens for connections on UNIX domain socket. You can specify the filesystem path to this UNIX domain socket to connect to.

## `-l, --lockless` ##
Don't use locking mechanism.

## `-e, --stop-on-error` ##
Stop programm execution on error.

## `-b, --background` ##
Start shell using non-interactive mode.

## `-q, --quiet` ##
Disable echo while executing commands from the file stream.

## `-d, --dry-run` ##
Don't actually execute ACTION scripts.

## `-x <path>, --xml-path=<path>` ##
Path to XML scheme files.

## `-w <view_name>, --view=<view_name>` ##
Set the startup view.

## `-i <vars>, --viewid=<vars>` ##
Set the startup viewid.

## `-u, --utf8` ##
Force UTF-8 encoding.

## `-8, --8bit` ##
Force 8-bit encoding.

## `-o, --log` ##
Enable command logging to syslog's local0.


# Environment #

# Files #

# Return codes #

The clish utility can return the following codes:

  * **0** - OK
  * **1** - Unknown internal error.
  * **2** - IO error. Can't find stdin for example.
  * **3** - Error while the [ACTION](ACTION.md) script execution.
  * **4** - Syntax error.
  * **255** - The system error like wrong command line option for clish utility.

# Notes #

The return codes are available since klish-1.5.2 or SVN's [revision #516](https://code.google.com/p/klish/source/detail?r=#516).