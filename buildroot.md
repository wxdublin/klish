

# Introduction #

Buildroot is a set of Makefiles and patches that makes it easy to generate a complete embedded Linux system. See the http://www.buildroot.net/ for the details. The klish can be used as the "package" with the buildroot environment to get into the buildroot's target embedded system.

# Details #

The klish source tree contain the contrib/buildroot directory with the files to embed the klish package into the buildroot environment. The contrib/buildroot/package/klish must be copied to the buildroot's source tree package/klish directory. Then the package/Config.in file must be changed. Add the following line

```
source "package/klish/Config.in"
```

to the section started with 'menu "Shell and utilities"' (or to the another
section if you think it will be better and you know what you do). After that you
can configure buildroot and enable the building the klish package. You can find
the menu for the klish within "Package Selection for the target"->"Shell and utilities" in the configurator. The klish's config allow to use the predefined version of klish or automatically download the last revision from the SVN repository.

These files were tested with buildroot-2010.11.
The current predefined stable version of klish package that used in the
buildroot's klish.mk file is 1.3.1.