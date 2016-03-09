

# Introduction #

The locking mechanism allows to execute several instances of clish utility (or another programs based on libclish library) simultaneously without conflicts. It's often usefull together with the [atomic actions](atomic_action.md).

# Details #

Before the command execution the klish engine try to get lock. The implementation of lock is a flock() call on the /tmp/clish.lock file. If process can't to get lock it repeats the attempts to get lock for the several times with the short sleep() beetween attempts. The fail means that someone got the lock earlier. If the process got lock it execute the command's ACTION and than unlock the file.

Some commands don't need the locking mechanism. The example of such command is 'ping'. It is independent command. The several 'ping's can be executed simultaneously. But the commands that can change the user config or some system settings need the locking mechanism. So the locking mechanism can be enabled/disabled on the per command basis. The [COMMAND](COMMAND.md) tag has the 'lock' field that can be 'true' or 'false'. It's 'true' but default. But if it's 'false' the klish engine will not try to get lock before this command execution.

The example of lockless 'ping' command:

```
        <COMMAND name="ping"
                help="Send messages to network hosts"
                lock="false">
        ...
        </COMMAND>
```

Sometimes it's needed to disable locking mechanism for the whole clish session. It's usefull if the clish utility is used from another clish instance from the command's ACTION. The command already got the lock so the nested clish can't get the lock. The nested clish can be executed with "-l" ( or "--lockless") option to disable locking mechanism.

The example of nested clish execution:

```
        <COMMAND name="nested"
                help="This command use nested clish utility">
               <ACTION>
               echo "ping www.google.com" | clish --lockless
               </ACTION>
        </COMMAND>
```