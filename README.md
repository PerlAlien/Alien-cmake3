# Alien::cmake3 ![linux](https://github.com/PerlAlien/Alien-cmake3/workflows/linux/badge.svg) ![windows](https://github.com/PerlAlien/Alien-cmake3/workflows/windows/badge.svg) ![macos](https://github.com/PerlAlien/Alien-cmake3/workflows/macos/badge.svg)

Find or download or build cmake 3 or better

# SYNOPSIS

From Perl:

```perl
use Alien::cmake3;
use Env qw( @PATH );

unshift @PATH, Alien::cmake3->bin_dir;
system 'cmake', ...;
```

From [alienfile](https://metacpan.org/pod/alienfile)

```perl
use alienfile;

share {
  # Build::CMake plugin pulls in Alien::cmake3 automatically
  plugin 'Build::CMake';
  build [
    # this is the default build step, if you do not specify one.
    [ '%{cmake3}', -G => '%{cmake_generator}', '-DCMAKE_POSITION_INDEPENDENT_CODE:BOOL=true', '-DCMAKE_INSTALL_PREFIX:PATH=%{.install.prefix}', '.' ],
    '%{make}',
    '%{make} install',
  ];
};
```

# DESCRIPTION

This [Alien](https://metacpan.org/pod/Alien) distribution provides an external dependency on the build tool `cmake`
version 3.0.0 or better.  `cmake` is a popular alternative to autoconf.

# METHODS

## bin\_dir

```perl
my @dirs = Alien::cmake3->bin_dir;
```

List of directories that need to be added to the `PATH` in order for `cmake` to work.

## exe

```perl
my $exe = Alien::cmake3->exe;
```

The name of the `cmake` executable.

# HELPERS

## cmake3

```
%{cmake3}
```

The name of the `cmake` executable.

# SEE ALSO

- [Alien::Build::Plugin::Build::CMake](https://metacpan.org/pod/Alien::Build::Plugin::Build::CMake)

    [Alien::Build](https://metacpan.org/pod/Alien::Build) plugin for `cmake`  This will automatically pull in Alien::cmake3 if you
    need it.

- [Alien::CMake](https://metacpan.org/pod/Alien::CMake)

    This is an older distribution that provides an alienized `cmake`.  It is different in
    these ways:

    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) is based on [alienfile](https://metacpan.org/pod/alienfile) and [Alien::Build](https://metacpan.org/pod/Alien::Build)

        It integrates better with [Alien](https://metacpan.org/pod/Alien)s that are based on that technology.

    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) will provide version 3.0.0 or better

        [Alien::CMake](https://metacpan.org/pod/Alien::CMake) will provide 2.x.x on some platforms where more recent binaries are not available.

    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) will install on platforms where there is no system `cmake` and no binary `cmake` provided by cmake.org

        It does this by building `cmake` from source.

    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) is preferred

        In the opinion of the maintainer of both [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) and [Alien::CMake](https://metacpan.org/pod/Alien::CMake) for these reasons.

# ENVIRONMENT

- ALIEN\_INSTALL\_TYPE

    This is the normal [Alien::Build](https://metacpan.org/pod/Alien::Build) environment variable and you can set it to one of
    `share`, `system` or `default`.

- ALIEN\_CMAKE\_FROM\_SOURCE

    If set to true, and if a share install is attempted, [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) will not try a
    binary share install (even if available), and instead a source share install.

# CAVEATS

If you do not have a system `cmake` of at least 3.0.0 available, then a share install
will be attempted.

Binary share installs are attempted on platforms for which the latest version of `cmake`
are provided.  As of this writing, this includes: Windows (32/64 bit), macOS
(intel/arm universal) and Linux (intel/arm 64 bit).  No checks are made to ensure that
your platform is supported by this binary installs.  Typically the same versions
supported by the operating system vendor and supported by `cmake`, so that should not
be a problem.  If you are using an operating system not supported by its vendor
Please Stop That, this is almost certainly a security vulnerability.

That said if you really do need [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) on an unsupported system,
you have some options:

- Install system version of `cmake`

    If you can find an older version better than 3.0.0 that is supported by your operating
    system.

- Force a source code install

    Set the `ALIEN_CMAKE_FROM_SOURCE` environment variable to a true value to build a
    share install from source.

Source share installs are attempted on platforms for which the latest version of
`cmake` are not available, like the various flavours of \*BSD.  This may not be ideal,
and if you can install a system version of `cmake` it may work better.

# AUTHOR

Author: Graham Ollis <plicease@cpan.org>

Contributors:

Adriano Ferreira (FERREIRA)

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
