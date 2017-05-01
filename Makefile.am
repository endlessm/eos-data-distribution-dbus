## Copyright 2017 Endless Mobile, Inc.

## This file is part of eos-data-distribution-dbus.
##
## eos-data-distribution-dbus is free software: you can redistribute it and/or
## modify it under the terms of the GNU Lesser General Public License as
## published by the Free Software Foundation, either version 2.1 of the
## License, or (at your option) any later version.
##
## eos-data-distribution-dbus is distributed in the hope that it will be
## useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
## MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
## GNU Lesser General Public License for more details.
##
## You should have received a copy of the GNU Lesser General Public
## License along with eos-data-distribution-dbus.  If not, see
## <http://www.gnu.org/licenses/>.

DISTCLEANFILES =
CLEANFILES =
EXTRA_DIST = debian README.md

AM_CFLAGS = $(LIBEOS_DATA_DISTRIBUTION_DBUS_CFLAGS)

INTROSPECTION_GIRS = EosDataDistributionDbus-@EDDD_API_VERSION@.gir
INTROSPECTION_SCANNER_ARGS = --warn-all --warn-error

eos-data-distribution-dbus-base-producer.h eos-data-distribution-dbus-base-producer.c: eos-data-distribution-dbus-base-producer.xml Makefile
	$(AM_V_GEN) $(GDBUS_CODEGEN) \
		--interface-prefix com.endlessm.DataDistribution. \
		--generate-c-code eos-data-distribution-dbus-base-producer \
		--c-namespace EosDataDistributionDbus \
		$<

eos-data-distribution-dbus-chunks-producer.h eos-data-distribution-dbus-chunks-producer.c: eos-data-distribution-dbus-chunks-producer.xml Makefile
	$(AM_V_GEN) $(GDBUS_CODEGEN) \
		--interface-prefix com.endlessm.DataDistribution. \
		--generate-c-code eos-data-distribution-dbus-chunks-producer \
		--c-namespace EosDataDistributionDbus \
		$<

eos_data_distribution_dbus_headers = \
	eos-data-distribution-dbus-base-producer.h \
	eos-data-distribution-dbus-chunks-producer.h \
	$(NULL)

eos_data_distribution_dbus_sources = \
	eos-data-distribution-dbus-base-producer.c \
	eos-data-distribution-dbus-chunks-producer.c \
	$(NULL)

edddincludedir = $(includedir)/@EDDD_API_NAME@/@PACKAGE_NAME@
edddinclude_HEADERS = $(eos_data_distribution_dbus_headers)

lib_LTLIBRARIES = libeos-data-distribution-dbus-@EDDD_API_VERSION@.la
libeos_data_distribution_dbus_@EDDD_API_VERSION@_la_CPPFLAGS = -Wall -Werror -I $(srcdir)
libeos_data_distribution_dbus_@EDDD_API_VERSION@_la_SOURCES = \
	$(eos_data_distribution_dbus_headers) \
	$(eos_data_distribution_dbus_sources) \
	$(NULL)
libeos_data_distribution_dbus_@EDDD_API_VERSION@_la_LIBADD = $(LIBEOS_DATA_DISTRIBUTION_DBUS_LIBS)
libeos_data_distribution_dbus_@EDDD_API_VERSION@_la_LDFLAGS = \
	-version-info @EDDD_LT_VERSION@ \
	$(AM_LDFLAGS) \
	$(NULL)

# Note that the template file is called eos-data-distribution-dbus.pc.in, but generates a
# versioned .pc file using some magic in AC_CONFIG_FILES, thanks to
# https://developer.gnome.org/programming-guidelines/unstable/parallel-installability.html.en#pkg-config
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = @EDDD_API_NAME@.pc

DISTCLEANFILES += $(pkgconfig_DATA)
EXTRA_DIST += eos-data-distribution-dbus.pc.in

include $(INTROSPECTION_MAKEFILE)

EosDataDistributionDbus-@EDDD_API_VERSION@.gir: libeos-data-distribution-dbus-@EDDD_API_VERSION@.la
EosDataDistributionDbus_@EDDD_API_VERSION@_gir_INCLUDES = GLib-2.0 Gio-2.0
EosDataDistributionDbus_@EDDD_API_VERSION@_gir_CFLAGS = $(AM_CFLAGS)
EosDataDistributionDbus_@EDDD_API_VERSION@_gir_LIBS = libeos-data-distribution-dbus-@EDDD_API_VERSION@.la
EosDataDistributionDbus_@EDDD_API_VERSION@_gir_FILES = \
	$(eos_data_distribution_dbus_headers) \
	$(eos_data_distribution_dbus_sources) \
	$(NULL)
EosDataDistributionDbus_@EDDD_API_VERSION@_gir_SCANNERFLAGS = \
	--identifier-prefix=eos_data_distribution_dbus_ \
	--identifier-prefix=EosDataDistributionDbus \
	$(NULL)

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)
typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)
CLEANFILES += $(gir_DATA) $(typelib_DATA)
