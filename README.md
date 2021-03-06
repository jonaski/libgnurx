:ox: libgnurx
=============

This is the regex functionality from glibc 2.33 extracted into a
separate library, for Win32. The original port was based on glibc
2.5, and the original README file (recorded below) is still of
high validity.

Updated to glibc 2.33 by [jonaski](https://github.com/jonaski)

Original regex from glibc 2.22 by:

--Timothy Gu  <timothygu99@gmail.com>

This is the regex functionality from glibc 2.5 extracted into a
separate library, for Win32.  It may be built, from the sources
provided, using the command sequence:--

  ./configure [--options...] && make

For a list of available configuration options, run:--

  ./configure --help

After building, as above, the resultant DLL, and optionally the
associated development kit, may be installed by:--

  make install

while redistributable binary DLL and development library kits may
be created by:--

  make dist


The original sources, on which this port is based, remain
copyright of their respective authors, or of the Free Software
Foundation Inc., as indicated in individual file headers; all are
redistributed with permission, as granted by the GNU Lesser
General Public License.

This is free software.  It is provided AS IS, in the hope that
it may be useful, but WITHOUT WARRANTY OF ANY KIND, not even an
IMPLIED WARRANTY of MERCHANTABILITY, nor of FITNESS FOR ANY
PARTICULAR PURPOSE.

Permission is granted to redistribute this software, either
"as is" or in modified form, under the terms of the GNU Lesser
General Public License, as published by the Free Software
Foundation; either version 2.1, or (at your option) any later
version.

You should have received a copy of the GNU Lesser General Public
License along with this software; see the file COPYING.LIB.  If
not, write to the Free Software Foundation, 51 Franklin St -
Fifth Floor, Boston, MA 02110-1301, USA.

The original port of this functionality was implemented by Tor
Lillqvist; I've adapted his work, to make it somewhat more MinGW
friendly.  I have *not* modified any of the `C' sources provided
by Tor; nor have I changed the naming conventions he adopted for
generated distributables.  I *have*:--

1) Replaced Tor's original `Makefile' with an autoconf generated
   configure script, and a backwardly compatible `Makefile.in';
   this provides a more flexible build procedure, which I find
   more convenient, when cross-compiling on a GNU/Linux host.

2) Added VPATH support, for `out of tree' builds.

3) Adapted the build procedure, to avoid a dependency on the `lib'
   program from Microsoft's MSVC tool chain.  This is achieved by
   providing an option to configure, which is disabled by default;
   it may by activated by specifying `--enable-msvc-implib' on the
   configure command line.  If this option is not activated, or if
   the MSVC `lib' tool is not present, the Makefile is configured
   without binding the rule for building an MSVC compatible import
   library, to the default target, (although the rule is left in
   place for explicit use).

   If the `--enable-msvc-implib' option is specified, but `lib' is
   not present, then configure will issue a warning message, and
   will again configure the Makefile without binding this rule to
   the default target.

   Only if the `--enable-msvc-implib' option is specified, *and*
   the `lib' tool is present, will building of an MSVC compatible
   import library be configured as a default deliverable.

4) Added `install', `install-dll' and `install-dev' targets, to
   support direct installation of the DLL, and its associated
   development kit.

5) Changed the default packaging format for distributables, from
   Tor's exclusive choice of `zip', to my own preferred `tar.gz';
   `zip' format remains available, as an option, by configuring
   with `--enable-dist=zip'.

6) Added `bindist', `devdist' and `srcdist' targets, for greater
   flexibility in building distribution kits.

The original text of Tor's README file will be found below.

--Keith Marshall  <keithmarshall@users.sourceforge.net>

I call the DLL libgnurx-0.dll which hopefully should be unique. At
least it isn't "regex.dll" which has been used by the
gnuwin32.sourceforge.net site for *two* incompatible DLLs. (That mess,
and the mess with their build of Henry Spencer's regex library, was
what lead me to build my own GNU regex library. See the
gnuwin32-users mailing list archives from December 2006.)

The "-0" is so that if at some point I build a release that isn't
binary compatible, I can then increment that and use a different name.

The import library for gcc is called libgnurx.dll.a, but I also
distribute a copy of it called libregex.a so that configure scripts
that look for -lregex will work.

Note that none of the wide-character and i18n functionality which is
built when this is part of glibc gets compiled. Thus things like
character classes most probably work only for single-byte codepages.

Compiling that stuff would drag in lots of glibc's locale handling
stuff which is completely incompatible with Microsoft's C library's
locale handling anyway. Also, I am not sure whether the GNU regex code
is prepared to handle a two-byte wchar_t, or does it assume that
wchar_t is int as it is on Linux? Hmm, actually there is lots of
sizeof(wchar_t) in glibc, so maybe it *is* prepared? Maybe
later... But anyway, it would presumably mean we should have not just
the regex functionality but a larger subset of glibc that would
include all locale, ctype, wchar, mbs, etc stuff, presumably ending up
with a very large part of glibc (not the system calls,
obviously). Indeed, something to save for later, or never...

--Tor Lillqvist <tml@iki.fi>, <tml@novell.com>
