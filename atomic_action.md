

# Introduction #

The [ACTION](ACTION.md) script can be interruptable or non-interruptable (atomic). It's often usefull together with the [locking mechanism](locking_mechanism.md).


# Details #

To make the action atomic the [ACTION](ACTION.md) script must be non-interruptable for the user. The following signals can be blocked while [ACTION](ACTION.md) script execution:
  * SIGINT
  * SIGQUIT
  * SIGHUP
So the user can't use Ctrl^C to terminate current process. The signal blocking is default behaviour for the [ACTION](ACTION.md) execution now. The signal blocking is implemented by sigprocmask() function. The blocked mask will be inherited by all executed processes.

To make action interruptable the [COMMAND](COMMAND.md) tag must contain interrupt="true" field. For example the 'ping' command may be interruptable.

```
        <COMMAND name="ping"
                help="Send messages to network hosts"
                interrupt="true">
        ...
        </COMMAND>
```

See the [COMMAND](COMMAND.md) field 'interrupt'. The atomic actions is available since SVN [revision 347](https://code.google.com/p/klish/source/detail?r=347) or klish-1.4.0. The SIGHUP signal is blocked since klish-1.5.6 and klish-1.6.1.

# Daemon execution #

Note when the [ACTION](ACTION.md) is non-interruptable the daemon execution within script is not safe enough because many services (daemons) use SIGHUP (or some another signals) for its work. For example the SIGHUP is signal to reread configuration files often. But when the [ACTION](ACTION.md) is non-interruptable the service will inherit signal mask from script so some signals will be masked and service will never get these signals. The right way to start services is to use special utility [sigexec](sigexec.md). This utility will unmask all signals and then execute command specified in its command line:

```
# sigexec /etc/init.d/vsftpd start
```

Use [sigexec](sigexec.md) utility everytime you start service and the service environment will be more suitable.