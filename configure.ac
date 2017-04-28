dnl Copyright 2017 Endless Mobile, Inc.

dnl This file is part of eos-data-distribution-dbus.
dnl
dnl eos-data-distribution-dbus is free software: you can redistribute it and/or
dnl modify it under the terms of the GNU Lesser General Public License as
dnl published by the Free Software Foundation, either version 2.1 of the
dnl License, or (at your option) any later version.
dnl
dnl eos-data-distribution-dbus is distributed in the hope that it will be
dnl useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
dnl GNU Lesser General Public License for more details.
dnl
dnl You should have received a copy of the GNU Lesser General Public
dnl License along with eos-data-distribution-dbus.  If not, see
dnl <http://www.gnu.org/licenses/>.

dnl Version numbers
dnl ---------------
dnl API name and version for pkg-config; increment when breaking API/ABI.
dnl This version number is also the major version number.
m4_define([_EDDD_API_VERSION_MACRO], [0])
dnl Before making a release, the three macros below should be modified.
dnl Minor and micro versions: increment micro version when making a release.
dnl Minor version is even for a stable release and odd for a development release.
dnl When making any release, if the API changes, set the interface age to 0.
m4_define([_EDDD_MINOR_VERSION_MACRO], [0])
m4_define([_EDDD_MICRO_VERSION_MACRO], [0])
m4_define([_EDDD_INTERFACE_AGE_MACRO], [0])
dnl Full version, for use in AC_INIT
m4_define([_EDDD_VERSION_MACRO],
    [_EDDD_API_VERSION_MACRO._EDDD_MINOR_VERSION_MACRO._EDDD_MICRO_VERSION_MACRO])

AC_INIT([eos-data-distribution-dbus], [_EDDD_VERSION_MACRO],
    [], [eos-data-distribution-dbus], [http://endlessm.com])
AM_INIT_AUTOMAKE([-Wall -Wno-portability foreign 1.11 tar-ustar no-dist-gzip dist-xz subdir-objects])
AM_SILENT_RULES([yes])

# Keep Autotools macros local to this source tree
AC_CONFIG_MACRO_DIR([m4])

# Variables to define
# -------------------
# Version numbers and associated macros
AC_SUBST([EDDD_API_VERSION], [_EDDD_API_VERSION_MACRO])
AC_DEFINE([EDDD_MAJOR_VERSION], [_EDDD_API_VERSION_MACRO], [Major (API) version])
AC_SUBST([EDDD_API_NAME], ["eos-data-distribution-dbus-$EDDD_API_VERSION"])
AC_DEFINE([EDDD_MINOR_VERSION], [_EDDD_MINOR_VERSION_MACRO], [Minor version])
AC_DEFINE([EDDD_MICRO_VERSION], [_EDDD_MICRO_VERSION_MACRO], [Micro version])

# Shared library versioning; calculated automatically.
# See http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html
EDDD_LT_CURRENT=m4_eval(100 * _EDDD_MINOR_VERSION_MACRO + _EDDD_MICRO_VERSION_MACRO - _EDDD_INTERFACE_AGE_MACRO)
EDDD_LT_REVISION=_EDDD_INTERFACE_AGE_MACRO
EDDD_LT_AGE=$EDDD_LT_CURRENT
AC_SUBST([EDDD_LT_VERSION], ["$EDDD_LT_CURRENT:$EDDD_LT_REVISION:$EDDD_LT_AGE"])

PKG_PROG_PKG_CONFIG

AC_PROG_MKDIR_P
AC_CACHE_SAVE

LT_INIT

AC_SUBST([EDDD_REQUIRED_MODULES_PUBLIC], [gio-unix-2.0])
PKG_CHECK_MODULES([LIBEOS_DATA_DISTRIBUTION_DBUS], [
    $EDDD_REQUIRED_MODULES_PUBLIC
])

GOBJECT_INTROSPECTION_REQUIRE([1.30])

# GDBus code generator
GDBUS_CODEGEN=`$PKG_CONFIG --variable gdbus_codegen gio-2.0`
AC_SUBST(GDBUS_CODEGEN)

AC_CONFIG_FILES([
    eos-data-distribution-dbus-$EDDD_API_VERSION.pc:eos-data-distribution-dbus.pc.in
    Makefile
], [], [EDDD_API_VERSION='$EDDD_API_VERSION'])
AC_OUTPUT
