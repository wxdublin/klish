

# Introduction #

The klish ([clish](utility_clish.md) console utility) supports UTF-8 and 8-bit encodings.

# Details #

The [clish utility](utility_clish.md) autodetects the current encoding using locale information. So the console input behaviour differs for UTF-8 and traditional 8-bit encodings.

If the locale is broken user can force using of the UTF-8 encoding by "-u" (--utf8) option on the clish's utility command line. The "-8" (--8bit) option is used to force 8-bit encoding.

The UTF-8 support is available since SVN [revision 345](https://code.google.com/p/klish/source/detail?r=345) or klish-1.4.0.