# FreeType Compilation Guide

FreeType's official git repository is located at

 - https://gitlab.freedesktop.org/freetype
 
from  which the  'freetype.git' and  'freetype-demos.git' repositories
can be cloned in the usual way.

 - `git clone https://gitlab.freedesktop.org/freetype/freetype.git`
 - `git clone https://gitlab.freedesktop.org/freetype/freetype-demos.git`

If you  want to  use the  Savannah mirror  instead, you  have to  do a
slightly different  incantation because  the repository  names contain
digit '2' for historical reasons.

  git clone \
    https://git.savannah.nongnu.org/git/freetype/freetype2.git \
    freetype
  git clone \
    https://git.savannah.nongnu.org/git/freetype/freetype2-demos.git \
    freetype-demos


## Building FreeType
There are  several ways  to build the  FreeType library,  depending on
your system and the level of  customization you need.  Here is a short
overview of the documentation available:


I. Prerequisites and dependencies
=================================

  FreeType is a low level C library  that only depends on the standard
  C library with very few platform-dependent optimizations utilized at
  build time.  System libraries, such as  zlib,  Gzip,  bzip2, Brotli,
  and libpng,  might  be  used  to handle  compressed fonts  or decode
  embedded PNG glyphs.

  FreeType  auto-configuration scripts  should be  able to detect  the
  prerequisites if the necessary headers are available  at the default
  locations.  Otherwise,  modify  `include/freetype/config/ftoption.h'
  to control how the FreeType library gets built.  Normally, you don't
  need to change anything.

  Applications have very limited control over FreeType's behaviour  at
  run-time;  look at the documentation of function `FT_Property_Set'.


II. Normal installation and upgrades
====================================

  1. Unix and Unix-like systems

    This also includes MacOS, Cygwin, MinGW + MSYS, Mingw-w64 + MSYS2,
    and possibly other, similar environments.

    Please read `INSTALL.UNIX' to install or upgrade FreeType  2 on  a
    Unix system.   Note  that  you  *need*  GNU  Make   for  automatic
    compilation,  since other make tools won't work (this includes BSD
    Make).

    GNU Make VERSION 3.81 OR NEWER IS NEEDED!

    [For `cmake' see below.]


  2. On VMS with the `mms' build tool

    See `INSTALL.VMS' for installation instructions on this platform.


  3. Other systems using GNU Make

    On some  non-Unix platforms, it  is possible to build  the library
    using only  the GNU Make utility.   Note that *NO OTHER  MAKE TOOL
    WILL  WORK*[1]!   This  methods   supports  several  compilers  on
    Windows, OS/2, and BeOS,  including MinGW* (without MSYS*), Visual
    C++, Borland C++, and more.

    Instructions are provided in the file `INSTALL.GNU'.


  4. With an IDE Project File (e.g., for Visual Studio or CodeWarrior)

    We provide a  small number of `project files'  for various IDEs to
    automatically build  the library as  well.  Note that  these files
    are  not supported  and only  sporadically maintained  by FreeType
    developers, so don't expect them to work in each release.

    To find them, have a  look at the content of the `builds/<system>'
    directory, where <system> stands for your OS or environment.


  5. Using cmake

    See the top-level `CMakeLists.txt' file for more information.


  6. From you own IDE, or own Makefiles

    If  you  want  to  create   your  own  project  file,  follow  the
    instructions   given  in  the   `INSTALL.ANY'  document   of  this
    directory.


III. Custom builds of the library
=================================

  Customizing the compilation  of FreeType is easy, and  allows you to
  select only the components of  the font engine that you really need.
  For more details read the file `CUSTOMIZE'.


----------------------------------------------------------------------

[1] make++, a make tool written in Perl, has sufficient support of GNU
    make extensions to build FreeType.  See

      https://makepp.sourceforge.net

    for more information;  you need version 2.0 or newer, and you must
    pass option `--norc-substitution'.


### Standard builds with `configure`

The git repository doesn't contain pre-built configuration scripts for
UNIXish platforms.  To generate them say

  sh autogen.sh

which in turn depends on the following packages:

  automake (1.10.1)
  libtool (2.2.4)
  autoconf (2.62)

The versions given  in parentheses are known to  work.  Newer versions
should  work too,  of course.   Note  that `autogen.sh`  also sets  up
proper file permissions for the `configure` and auxiliary scripts.

The `autogen.sh` script checks whether the versions of the above three
tools match the numbers above.  Otherwise it will complain and suggest
either  upgrading or  using  environment variables  to  point to  more
recent versions of the required tools.

Note that  `aclocal` is provided  by the 'automake' package  on Linux,
and that `libtoolize` is called `glibtoolize` on Darwin (OS X).


## Alternative build methods

For static  builds that don't use  platform-specific optimizations, no
configure script is necessary at all; saying

  make setup ansi
  make

should work on all platforms that have GNU `make` (or `makepp`).

A build  with `cmake`  or `meson`  can be done  directly from  the git
repository.  However, if you want  to use the `FT_DEBUG_LOGGING` macro
(see file `docs/DEBUG` for more information) it is currently mandatory
to execute `autogen.sh`  in advance; this script clones  the 'dlg' git
submodule and copies some files into FreeType's source tree.


<details>
<summary>Copyright Notice</summary>

```
Copyright (C) 2000-2021 by
David Turner, Robert Wilhelm, and Werner Lemberg.

This  file is  part of  the FreeType  project, and  may only  be used,
modified,  and distributed  under the  terms of  the  FreeType project
license,  COPYING.md.  By  continuing to  use, modify,  or distribute
this file you  indicate that you have read  the license and understand
and accept it fully.
```
</details>
