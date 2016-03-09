

# Introduction #

The key combinations (hotkeys) can be programmed to execute specified actions. Use [HOTKEY](HOTKEY.md) tag to define hotkey and its action.

# Details #

All [VIEW](VIEW.md)s (including global implicit [VIEW](VIEW.md)) can contain [HOTKEY](HOTKEY.md) tag to define hotkey for this [VIEW](VIEW.md). If the nested [VIEW](VIEW.md)s are used the klish engine will search for hotkey definition in the current [VIEW](VIEW.md), then in the upper [VIEW](VIEW.md) and so on. So you can define [HOTKEY](HOTKEY.md) within global [VIEW](VIEW.md) and all other [VIEW](VIEW.md)s will share this definition.

See the example:
```
<HOTKEY key="^Z" cmd="exit"/>

<VIEW name="enable_view" ...>
        ...
        <HOTKEY key="^@" cmd="show"/>
        ...
</VIEW>

<VIEW name="configure-view" ...>
        ...
        <HOTKEY key="^@" cmd="do show"/>
        ...
</VIEW>
```

This example defines two hotkeys. The "`Ctrl^Z`" for exit. It is defined in the global [VIEW](VIEW.md) and will act in the all [VIEW](VIEW.md)s (in a case it will not be redefined in the nested [VIEW](VIEW.md)s).

The second hotkey is "`Ctrl^@`". Both "`Ctrl^@`" and "`Ctrl^spacebar`" combinations give this key code. This hotkey will execute "show" command in the "enable-view" [VIEW](VIEW.md) and all its subviews but the "do show" command in "configure-view" [VIEW](VIEW.md) and all its subviews.

# Possible keys #

Some keys has predefined hardcoded behaviour. If key has a predefined behaviour it can't be redefined (used in [HOTKEY](HOTKEY.md) tag) now.

| **Code** | **Id** | **Key** | **Action** | **Comment** |
|:---------|:-------|:--------|:-----------|:------------|
| 0        | NUL    | ^@      |            | Null character |
| 1        | SOH    | ^A      | Home       | Start of heading, = console interrupt |
| 2        | STX    | ^B      |            | Start of text, maintenance mode on HP console |
| 3        | ETX    | ^C      | Break      | End of text |
| 4        | EOT    | ^D      | Delete     | End of transmission, not the same as ETB |
| 5        | ENQ    | ^E      | End        | Enquiry, goes with ACK; old HP flow control |
| 6        | ACK    | ^F      |            | Acknowledge, clears ENQ logon hand |
| 7        | BEL    | ^G      |            | Bell, rings the bell... |
| 8        | BS     | ^H      | Backspace  | Backspace, works on HP terminals/computers |
| 9        | HT     | ^I      | Tab        | Horizontal tab, move to next tab stop |
| 10       | LF     | ^J      | Enter      | Line Feed   |
| 11       | VT     | ^K      | Kill line  | Vertical tab |
| 12       | FF     | ^L      | Clear screen | Form Feed, page eject |
| 13       | CR     | ^M      | Enter      | Carriage Return |
| 14       | SO     | ^N      |            | Shift Out, alternate character set |
| 15       | SI     | ^O      |            | Shift In, resume defaultn character set |
| 16       | DLE    | ^P      |            | Data link escape |
| 17       | DC1    | ^Q      |            | XON, with XOFF to pause listings; "okay to send". |
| 18       | DC2    | ^R      |            | Device control 2, block-mode flow control |
| 19       | DC3    | ^S      |            | XOFF, with XON is TERM=18 flow control |
| 20       | DC4    | ^T      |            | Device control 4 |
| 21       | NAK    | ^U      | Erase line | Negative acknowledge |
| 22       | SYN    | ^V      |            | Synchronous idle |
| 23       | ETB    | ^W      | Erase word | End transmission block, not the same as EOT |
| 24       | CAN    | ^X      |            | Cancel line, MPE echoes !!! |
| 25       | EM     | ^Y      | Yank       | End of medium, Control-Y interrupt |
| 26       | SUB    | ^Z      |            | Substitute  |
| 27       | ESC    | ^[      | Escape     | Escape, next character is not echoed |
| 28       | FS     | ^\      |            | File separator |
| 29       | GS     | ^]      |            | Group separator |
| 30       | RS     | ^^      |            | Record separator, block-mode terminator |
| 31       | US     |`^_`     |            | Unit separator |