AC_PREREQ(2.59)

AC_INIT([iio-sensor-proxy], [1.1], [hadess@hadess.net])

AX_IS_RELEASE([git-directory])

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE(1.9 dist-xz no-dist-gzip check-news)

# Enable silent build when available (Automake 1.11)
m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_INSTALL
AC_PROG_SED
AM_PROG_CC_C_O

AX_COMPILER_FLAGS([WARN_CFLAGS],[WARN_LDFLAGS])

GTK_DOC_CHECK([1.11],[--flavour no-tmpl])

AC_ARG_WITH([udevrulesdir],
	    AS_HELP_STRING([--with-udevrulesdir=DIR], [Directory for udev rules]),
	    [],
	    [with_udevrulesdir=$($PKG_CONFIG --variable=udevdir udev)"/rules.d"])
AC_SUBST([udevrulesdir], [$with_udevrulesdir])

AC_ARG_WITH([systemdsystemunitdir],
	    AS_HELP_STRING([--with-systemdsystemunitdir=DIR], [Directory for systemd service files]),
	    [],
	    [with_systemdsystemunitdir=$($PKG_CONFIG --variable=systemdsystemunitdir systemd)])
if test x$with_systemdsystemunitdir != xno; then
	AC_SUBST([systemdsystemunitdir], [$with_systemdsystemunitdir])
fi

PKG_CHECK_MODULES(IIO_SENSOR_PROXY, gio-2.0 gudev-1.0)

AC_PATH_PROG([GDBUS_CODEGEN],[gdbus-codegen])

AC_CONFIG_FILES([
	Makefile
	data/Makefile
	src/Makefile
	docs/Makefile
	docs/version.xml
])
AC_OUTPUT
