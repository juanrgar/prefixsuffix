# Put compiled object files into the same sub-directory as their sources
AUTOMAKE_OPTIONS = subdir-objects

# Point to our macro directory and pick up user flags from the environment
ACLOCAL_AMFLAGS  = -I macros ${ACLOCAL_FLAGS}

# Make warnings always fatal at distcheck time, and disable execution
# of tools that change files not installed by the package itself
DISTCHECK_CONFIGURE_FLAGS = --enable-warnings=fatal --disable-update-mime-database

SUBDIRS = po help docs


AM_CXXFLAGS = $(PREFIXSUFFIX_WXXFLAGS)

bin_PROGRAMS = prefixsuffix

#List of source files needed to build the executable:
prefixsuffix_SOURCES = \
	src/main.cc \
	src/application.h \
	src/application.cc \
	src/mainwindow.h \
	src/mainwindow.cc \
	src/renamer.h \
	src/renamer.cc \
	src/bakery/Configuration/Association.h \
	src/bakery/Configuration/Association.cc \
	src/bakery/Configuration/AssociationBase.h \
	src/bakery/Configuration/AssociationBase.cc \
	src/bakery/Configuration/Client.h \
	src/bakery/Configuration/Client.cc \
	src/bakery/Utilities/sharedptr.h
	
EXTRA_DIST = \
	data/prefixsuffix-logo.png \
	data/prefixsuffix.glade

gladedir = $(datadir)/prefixsuffix/glade/

# Let the code know where the glade dir is:
prefixsuffix_CXXFLAGS = $(DEPS_CFLAGS) \
	-I$(top_builddir)/src -I$(top_srcdir)/src \
	-I$(top_builddir) -I$(top_srcdir) \
	-DPREFIXSUFFIX_GLADEDIR=\""$(gladedir)/"\"
prefixsuffix_LDADD = $(DEPS_LIBS)



# Desktop entry
desktopdir		= $(datadir)/applications
desktop_DATA 		= data/prefixsuffix.desktop
@INTLTOOL_DESKTOP_RULE@

# Icon
icondir = $(datadir)/pixmaps
icon_DATA = prefixsuffix.png

# GSettings schemas, enum files and conversion file
#gsettings_ENUM_NAMESPACE = org.gnome.prefixsuffix
#gsettings_ENUM_FILES = $(top_srcdir)/src/*.h $(top_srcdir)/src/backend/*.h
gsettings_SCHEMAS = data/org.gnome.prefixsuffix.gschema.xml
@GSETTINGS_RULES@

EXTRA_DIST += $(desktop_DATA) $(icon_DATA) \
             intltool-extract.in intltool-merge.in intltool-update.in


# Install the glade file:
# The glade prefix of glade_DATA seems to cause it to be installed in <appname>/glade/
# Because that's how gladedir is defined.
glade_DATA = data/prefixsuffix.glade
EXTRA_DIST += $(glade_DATA)

