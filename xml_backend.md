

# XML backends #

The klish engine uses external (since version klish-1.6.0) XML backends to parse XML config files. Now klish supports three XML backends:

  * libxml2
  * expat
  * libroxml

There are XML tests in xml-examples/test directory in klish sourcecode tree. These tests contain some typical cases that can lead to XML backend errors.

You can specify preferred XML backend by project configure script argument:

  * --with-libxml2 for using libxml2
  * --with-libexpat for using expat
  * --with-libroxml for using libroxml

## libxml2 ##
The libxml2 project homepage is http://www.xmlsoft.org/.
The tested versions are:
### 2.7.8 ###
The klish-1.6.0 tests are passed on:
  * Linux (ArchLinux)
  * FreeBSD 8.2

## expat ##
The expat project homepage is http://expat.sourceforge.net/.
The tested versions are:
### 2.0.1 ###
The klish-1.6.0 tests are passed on:
  * Solaris 11
  * FreeBSD 8.2
### 2.1.0 ###
The klish-1.6.0 tests are passed on:
  * Linux (ArchLinux)

## libroxml ##
The expat project homepage is [https://code.google.com/p/libroxml/. Don't use versions earlier than libroxml-2.2.0.
The tested versions are:

### 2.1.1 ###
> The klish-1.6.0 test are passed.
  * FreeBSD 8.2
> Probably the recent version of libroxml can be build on this systems.

### 2.2.0 ###
> The klish-1.6.0 tests are NOT passed. The "test5" is failed (broken quotes within comment). Now libroxml git repository contain the patch to solve this problem. It was tested on:
  * Linux (ArchLinux)

# Legacy backend #

The klish earlier than klish-1.6.0 version uses internal implementation of [tinyXML](http://sourceforge.net/projects/tinyxml/) engine. It was frozen snapshot and it was rather good but tinyXML is written in C++. So klish can't be build without C++. It's not good for embedded devices. The klish-1.6.0 and later versions can be build without C++.

# FreeBSD note #

The FreeBSD use "ports" system for third party open source projects. All ports are installed to /usr/local. So the klish configuration with installed XML backends is something like this:
```
# CPPFLAGS="-I/usr/local/include" LDFLAGS="-L/usr/local/lib" ./configure --with-libxml2
```

# Solaris note #

The Solaris 11 has no pkg-config package. The configure script use pkg-config to search for libxml2 headers and libs. So to build klish with libxml2 backend you need to configure libxml2 path manually:
```
# ./configure --with-libxml2=/usr
```