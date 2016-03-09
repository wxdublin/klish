

# Introduction #

The parameters can be nested i.e. [PARAM](PARAM.md) can contain another sub-PARAMs.

# Details #

The sub-parameters will be taken into account then the parent parameter is set. If the parent parameter is not set cause it's [optional](optional_arguments.md) or then engine choose another execution way while [branching](switch_subcommand.md) the sub-paremeters will not be taken into account and the corresponding variables will be unset. After analyzing sub-parameters engine will continue the normal flow and will analyze the next parameter after parent parameter (which contain sub-parameters).

There is a good example of using nested parameters in [optional parameters](optional_arguments.md) page. See the klish native variant. Another good example of nesting you can find in [switch subcommand](switch_subcommand.md) page.