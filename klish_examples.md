

# Introduction #

The klish source tree contain the klish specific XML examples that show the basic CISCO-like (not exactly copy) interface to configure network interfaces and routing on Linux system. You can find it in xml-examples/klish dir in the klish source tree.

The original clish examples is also available and workable. You can find it in xml-examples/clish dir.

# The KLISH specific examples #

The klish has some new features that is not supported in clish. So the klish specific examples show some of these new features. The dir xml-examples/klish is more complex than clish examples dir. That is needed to show CISCO-like 'enable' command that allow to get privileged mode and execute administration commands.

## The 'enable' command implementation ##

The 'enable' command is implemented by using 'su' linux command and executing new clish instance. It's the right way to get privilegies because the clish/klish is not enough tool to distribute system permissions. When the 'su -c clish' is used the operation system is responsible to permit or deny some system operations to the current user. For example unprivileged user cannot change the network interfaces settings and routing table. So if even the unprivileged user will be able to enter network specific commands in klish the system will deny his commands.

If the some kind of role model is needed the 'su' command can be used to became non-root user with additional permissions. The additional permissions can be set using 'sudo' for example.

## Directory structure ##

The directory structure resulting from the realization of 'enable' command. The privileged and unprivileged users must have the different set of XML files. The example suppose that klish was configured with './configure --prefix=/usr' so the installed clish binary will be located in /usr/bin dir. The 'etc' dir of the example must be copied to the / dir to the target system.

The etc/ dir contain clish/ clish-enable/ and clish-xml/ dirs. The clish-xml/ dir contain the all (privileged and unprivileged) XMLs. The clish/ dir contain symbolic links to the ../clish-xml/`<name>`.xml files that is needed in non-privileged mode. The clish-enable/ dir contain symbolic links to the ../clish-xml/`<name>`.xml files that is needed in privileged mode.

The etc/ also contain init.d/klish-init script that will init klish subsystem on the boot time. It starts the konfd daemon that will store all the configuration (all the configuration commands user will enter). Then the saved configuration file /etc/startup-config is executed via klish to restore previous (pre-reboot) system configuration. The init.d/klish-init script can be included in some init script like rc.local so it will be executed automatically on system startup.

## The testing purposes only ##

If you don't want to install all klish infrastructure to your system and don't want to use 'enable' command you can use the following commands to see the ability of unprivileged and privileged examples (suppose the current dir is a klish source tree):

```
~/klish$ CLISH_PATH=xml-examples/klish/etc/clish bin/clish
~/klish$ CLISH_PATH=xml-examples/klish/etc/clish-enable bin/clish
```

Note privileged commands can be entered by the common user but the real system commands execution will be denied.

# The CLISH original examples #

To test klish over the clish original examples the project must be configured and built. Unarchive the source code tarball and 'cd' to the klish-`<version>` tree. Then execute the following commands:

```
$ ./configure
$ make
$ CLISH_PATH=xml-examples/clish bin/clish
```