# Alien::cmake3 [![Build Status](https://secure.travis-ci.org/plicease/Alien-cmake3.png)](http://travis-ci.org/plicease/Alien-cmake3)

Find or download or build cmake 3 or better

# SYNOPSIS

From Perl:

    use Alien::cmake3;
    use Env qw( @PATH );
    
    unshift @PATH, Alien::cmake->bin_dir;
    system 'cmake', ...;

From [alienfile](https://metacpan.org/pod/alienfile)

    use alienfile;
    
    share {
      requires Alien::cmake3;
      build [
        '%{cmake3} ...'
        '%{make}',
        '%{make} install',
      ],
    };

# DESCRIPTION

This [Alien](https://metacpan.org/pod/Alien) distribution provides an external dependency on the build tool `cmake`
version 3.0.0 or better.  `cmake` is a popular alternative to autoconf.

# METHODS

## bin\_dir

    my @dirs = Alien::cmake3->bin_dir;

List of directories that need to be added to the `PATH` in order for `cmake` to work.

## exe

    my $exe = Alien::cmake3->exe;

The name of the `cmake` executable.

# HELPERS

## cmake3

    %{cmake3}

The name of the &lt;cmake> executable.

# SEE ALSO

- [Alien::CMake](https://metacpan.org/pod/Alien::CMake)

    This is an older distribution that provides an alienized `cmake`.  It is different in
    these ways:

    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) is based on [alienfile](https://metacpan.org/pod/alienfile) and [Alien::Build](https://metacpan.org/pod/Alien::Build) and integrates better with [Alien](https://metacpan.org/pod/Alien)s that are based on that technology.
    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) will provide version 3.0.0 or better.  [Alien::CMake](https://metacpan.org/pod/Alien::CMake) will provide 2.x.x on some platforms where more recent binaries are not available.
    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) will install on platforms where there is no system `cmake` and no binary `cmake` provided by cmake.org.  It does this by building `cmake` from source.
    - [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) is preferred in the opinion of the maintainer of both [Alien::cmake3](https://metacpan.org/pod/Alien::cmake3) and [Alien::CMake](https://metacpan.org/pod/Alien::CMake) for these reasons.

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
