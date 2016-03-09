

# Introduction #

The HOWTO.

# The XML files validation #

The XML files can be validated by the xmllint utility.
```
        $xmllint --noout --schema <schema_filename>.xsd <xml_filename>.xml
```
Or you can validate all XML file in the specified dir:
```
        $xmllint --noout --schema <schema_filename>.xsd <xml_dir>/*.xml
```

# Static build #

To build klish statically use:
```

$ ./configure --disable-shared
$ make LDFLAGS+="-all-static"
```

The LDFLAGS is global so shared libraries can't be build and building of shared libraries must be disabled.

# Leak of dlopen() #

If target system doesn't support dlopen() then configure script will configure building process to don't use dlopen() (and other dl functions) but link to plugin's shared objects.

If you need to link statically with plugins use:
```

$  ac_cv_header_dlfcn_h=no ./configure --prefix=/usr --with-lua --disable-shared
$ make LDFLAGS+="-all-static"
```