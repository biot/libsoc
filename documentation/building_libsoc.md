# Building libsoc

libsoc uses the GNU Autotools build system to configure and compile the library. Autotools was chosen as it is a very well supported and mature build system. It can cross-compile code with minimal fuss and includes many useful features.

---

### Setting up Autotools

First, ensure that your distro has the autotools suite installed. You can check this by making sure the binaries autoconf and automake can be found. Once confirmed these tools are available you can either run the script `autogen.sh` from the root of the libsoc git repo or run `autoreconf -i` to install the autotools environment to the directory.

---

### Running Configure

Once your autotools environment is fully setup as per above, you can then move onto configuring the options with which to build the library. This is the point where you can configure additional libsoc features, set your cross compile tools and set your installation paths.

libsoc allows the use of all the standard `configure` arguments and examples of these can be found in the autotools manual or in one of the numerous autotool tutorials around the web.

libsoc also add somes additional configure options to control certain library features.

`--with-board-configs`

Installs all the board configuration files in contrib/board_files to $(pkgdatadir) when performing a `make install`.

`--enable-board=board`

When used in conjunction with `--with-board-configs` it will create a symlink from $(sysconfdir)/libsoc_gpio.conf to $(pkgconfigdir)/board/libsoc_gpio.conf

When not used in conjunction with `--with-board-configs` it will install the board configuration file from contrib/board_configs/board/libsoc_gpio.conf to $(sysconfdir)

`--disable-debug`

Disables the compiling and inclusion of the debug functions. Should only be used to try squeeze the very last of performance improvements out of the library.

#### Examples

- Plain configure, no extra features enabled, building for the host architecture, and installing with the prefix directory prefix '/usr', as opposed to the default '/usr/local'.

`./configure --prefix=/usr`

- Configure and install board configurations, but don't setup a default configuration file. Useful for creating non board-specific packages, but also allow the user to manually use a shipped config.

`./configure --with-board-configs`

- Configure and install a single board configuration to be used by default. Useful for when a package is built for a specific board. The example sets the beaglebone config to be installed.

`./configure --enable-board=beaglebone`

---

### Running Make

Once properly configured you can then compile the library by running a simple `make`. Then to install the library into the system dirs, a `make install` will suffice.

---

[Return to Index](README.md)
