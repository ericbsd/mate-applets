AM_CPPFLAGS = \
	$(MATE_APPLETS4_CFLAGS) \
	-I$(srcdir) \
	-DMATELOCALEDIR=\""$(prefix)/$(DATADIRNAME)/locale"\" \
	$(DISABLE_DEPRECATED_CFLAGS)

APPLET_LOCATION = $(libexecdir)/command-applet

libexec_PROGRAMS = command-applet
command_applet_SOURCES = command.c
command_applet_LDADD = $(MATE_APPLETS4_LIBS)
command_applet_CFLAGS = $(WARN_CFLAGS)

appletsdir       = $(datadir)/mate-panel/applets
applets_in_files = org.mate.applets.CommandApplet.mate-panel-applet.in
applets_DATA     = $(applets_in_files:.mate-panel-applet.in=.mate-panel-applet)

$(applets_in_files): $(applets_in_files).in Makefile
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
		$< > $@
%.mate-panel-applet: %.mate-panel-applet.in $(INTLTOOL_MERGE) $(wildcard $(top_srcdir)/po/*po) ; $(INTLTOOL_MERGE) $(top_srcdir)/po $< $@ -d -u -c $(top_builddir)/po/.intltool-merge-cache

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.CommandAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

org.mate.panel.applet.CommandAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
		$< > $@

@INTLTOOL_XML_NOMERGE_RULE@
gsettings_SCHEMAS = org.mate.panel.applet.command.gschema.xml
@GSETTINGS_RULES@

%.gschema.xml.in: %.gschema.xml.in.in Makefile
	$(AM_V_GEN) $(SED) -e 's^\@GETTEXT_PACKAGE\@^$(GETTEXT_PACKAGE)^g' < $< > $@

EXTRA_DIST = \
	$(applets_in_files) \
	$(service_in_files) \
	$(gsettings_SCHEMAS).in.in
