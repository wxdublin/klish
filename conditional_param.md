

# Introduction #

The [parameter](PARAM.md) can be dynamically enabled or disabled depending on the condition. The condition have the syntax same as standard /bin/test utility. So the [parameter](PARAM.md) visibility can depend on the previous [parameters](PARAM.md) values.

# Details #

The [PARAM](PARAM.md) tag has the optional 'test' field. The 'test' field contains the expression to evaluate. If the expression is evaluated to false the PARAM does not appear at CLI shell and the ${param\_name} variable will be empty. If the [PARAM](PARAM.md) is disabled you can consider it as the parameter is not exists. The [internal variables](internal_variables.md) and previous [parameters](PARAM.md) values can be used within expression. The following syntax is used to construct expression (from OpenBSD man pages):

> -n string
> > True if the length of string is nonzero.

> -z string
> > True if the length of string is zero.

> s1 = s2
> > True if the strings s1 and s2 are identical.

> s1 != s2
> > True if the strings s1 and s2 are not identical.

> s1 < s2
> > True if string s1 comes before s2 based on the ASCII value of
> > their characters.

> s1 > s2
> > True if string s1 comes after s2 based on the ASCII value of
> > their characters.

> s1      True if s1 is not the null string.
> n1 -eq n2
> > True if the integers n1 and n2 are algebraically equal.

> n1 -ne n2
> > True if the integers n1 and n2 are not algebraically equal.

> n1 -gt n2
> > True if the integer n1 is algebraically greater than the integer
> > n2.

> n1 -ge n2
> > True if the integer n1 is algebraically greater than or equal to
> > the integer n2.

> n1 -lt n2
> > True if the integer n1 is algebraically less than the integer n2.

> n1 -le n2
> > True if the integer n1 is algebraically less than or equal to the
> > integer n2.

> These primaries can be combined with the following operators.  The -a
> operator has higher precedence than the -o operator.
> ! expression
> > True if expression is false.

> expression1 -a expression2
> > True if both expression1 and expression2 are true.

> expression1 -o expression2
> > True if either expression1 or expression2 are true.

> ( expression )
> > True if expression is true.

The example demonstrate the parameter "size" that will be enabled if "proto" is "ip" or "ipv6" and will be disabled if proto is "arp".

```
        <COMMAND name="ping"
                help="Send messages to network hosts">
                <PARAM name="proto"
                        help="Protocol to use for the ping"
                        optional="true"
                        mode="switch"
                        ptype="SUBCOMMAND">
                        <PARAM name="ip"
                                help="Send ICMP IPv4 messages to network hosts (default)"
                                mode="subcommand"
                                ptype="SUBCOMMAND"/>
                        <PARAM name="ipv6"
                                help="Send ICMP IPv6 messages to network hosts"
                                mode="subcommand"
                                ptype="SUBCOMMAND"/>
                        <PARAM name="arp"
                                help="Send ARP requests to a neighbour host"
                                mode="subcommand"
                                ptype="SUBCOMMAND"/>
                </PARAM>

                ...

                <PARAM name="size"
                        test='"${proto}"!="arp"'
                        help="Packet size"
                        optional="true"
                        mode="subcommand"
                        ptype="SUBCOMMAND">
                        <PARAM name="psize"
                                help="Number of data bytes to send"
                                ptype="UINT"/>
                </PARAM>

                ...

                </COMMAND>
```