

# Introduction #

The konfd is a daemon to store current running-config. You can consider running-config as a current system settings or as a list of commands that have been executed for now by the user or automatically (by the script).

The name "konfd" is used since klish-1.1.0. The earlier versions use name "confd" for the configuration daemon.

# The running-config #

Generally the running-config consists of the the arbitrary text lines. Each entry may contain another nested text lines. Note the **konfd knows nothing about klish commands and klish syntax**. The commands is just a **text strings** for the konfd. It's important to realize. The example of running-config:

```

hostname Router
!
interface ethernet 0
ip address 192.168.1.1/24
enable
!
interface ethernet 1
ip address 10.0.0.1
```

The "hostname Router" entry has no nested entries. The "interface ethernet 0" and "interface ethernet 1" contain nested entries.

## Comments ##
The "!" symbol is a comment for the klish. Each line starting with the "!" consider as a comment so this line will be ignored by the klish. The konfd daemon can output a current state of running-config. The previous text is an example of such output. Generally the comments are not really stored by the konfd. The konfd automatically inserts "!" beetween first level running-config entries for more human readable view.

## Path ##
The running-config structure can be considered as a filesystem-like structure. The "interface ethernet 0" entry can be considered as a directory with the nested "files". So each entry has a "path". The first level entries have an empty path but the nested entries like a "enable" entry has a non-empty path:
```

"interface ethernet 0"
```
The running-config can contain multi level nesting:
```

interface ethernet 0
ip address 192.168.1.1/24
ip options
mtu 1500
enable
```
In this case the "mtu 1500" entry has a following path:
```

"interface ethernet 0" "ip options"
```
The "path" concept is important for running-config entries manipulations.

## Priority ##

Each entry has a priority. The priority is a 16-bit unsigned integer. The entries with minimal priority resides on the begining of the running-config. The default priority is "0". The entries with the same priority will be ordered alphabetically.

The priority can be specified in hex format. The klish use "0x7f00" default value for the priority if priority is not specified explicitly within [CONFIG](CONFIG.md) tag. The "0x7f00" is a middle of the possible priority range.

The high and low bytes within priority value have a little different meanings. The first level entries with different high bytes will be splitted by "!" (comment sign) always. By default the entries with equal high byte and arbitrary low byte will be splitted by "!" too. But if the entry has a "non-split" flag (see konfd protocol description to find out how to set this flag) the "!" will not be inserted before current entry if previous entry has the same high byte. So the entries can be grouped and don't be splitted by the "!".

The high and low bytes within priority value have no special meanings for nested entries.

## Sequences ##

The konfd supports ordered lists a.k.a. "sequences". The entry can be or not to be a part of the sequence. It can be specified by a special options while entry creation. All entries in sequence must have the same priority value. The priority can be considered as an identifier of the sequence. The running-config can contain many sequences at the same time. The sequences will be identified by the priority value.

The new entry can be inserted into sequence with specified sequence number. The entry can be removed from the sequence by its sequence number.

The konfd can output entries without or with sequence numbers prepending the entry value.

See the konfd communication protocol description for detail about sequence using.

# Communicate to konfd daemon #

The konfd daemon is accessible via UNIX socket interface. The socket path can be specified via command line. So it's possible to have a several konfd executed simultaneously. The default socket path is /tmp/konfd.socket.

The konfd uses text based protocol for communication with another processes. The syntax of protocol is like a command line with options. It will be documented later in this document.

# Options #

## `-v, --version` ##
Print the version of clish utility.

## `-h, --help` ##
Print help.

## `-d, --debug` ##
Enable debug mode. Don't daemonize konfd.

## `-s <path>, --socket=<path>` ##
Specify the UNIX socket filesystem path to listen on.

## `-p <path>, --pid=<path>` ##
File to save daemon's PID to.

## `-r <path>, --chroot=<path>` ##
Path to chroot to. Used for security reasons.

## `-u <user>, --user=<user>` ##
Execute daemon as specified user.

## `-g <group>, --group=<group>` ##
Execute process as specified group.

# The konfd protocol #
The syntax of protocol is like a command line with options. The actions and options are specified by the arguments prepend with "-" or "--" (for long options) and after all arguments the "path" is specified. Each element of path must be quoted. Firstly the action must be specified:

## Add entry: `-s, --set` ##
To add new entry to the running-config the `"-s"` or `"--set"` argument is used. The following arguments are mandatory for this action:
  * `-l <string>, --line=<string>`. This argument defines the text line to add to the running-config.
  * `-r <regexp>, --pattern=<regexp>`. This argument contain extended regular expression and defines unique part of the entry i.e. the existing entries matching this pattern will be removed before new entry creation.
  * The path to store new entry. This argument can be empty if entry must be added to the first level.

Examples:
```

-s -l "interface ethernet 0" -r "^interface ethernet 0$"
```
This example will add new entry "interface ethernet 0" to the first level of the running-config. If the entry "interface ethernet 0" already exists it will be overwritten by the same entry. The definitions of another interfaces (with another interface numbers) will not be removed because the regular expression contain the number "0" at the end of the pattern.

```

-s -l "ip address 192.168.0.1/24" -r "^ip address " "interface ethernet 0"
```
This example will add new nested entry "ip address 192.168.0.1/24" to the "interface ethernet 0" path. If the IP-address was defined before this action the old entry matching the "^ip address " pattern will be replaced by the new address. Suppose the entry "interface ethernet 0" already exists.

```

-s -l "mtu 1500" -r "^mtu " "interface ethernet 0" "ip options"
```
This code will add "mtu 1500" nested entry to the path "interface ethernet 0" "ip options". Suppose the path entries already exist. The running-config output after this operation is:
```

interface ethernet 0
ip options
mtu 1500
```