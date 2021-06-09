SUBDIRS = lib/libalpm

DIST_SUBDIRS = $(SUBDIRS)

ACLOCAL_AMFLAGS = -I m4 --install
AM_MAKEFLAGS = --no-print-directory

# Make sure we test and build manpages when doing distcheck
DISTCHECK_CONFIGURE_FLAGS = --disable-git-version \
		bashcompdir='$${prefix}/share/bash-completion/completions'

EXTRA_DIST = \
	HACKING test/tap.sh \
	build-aux/edit-script.sh.in \
	build-aux/script-wrapper.sh.in


# Sample makepkg prototype files
pkgdatadir = ${datadir}/${PACKAGE}

LOG_DRIVER = env AM_TAP_AWK='$(AWK)' $(SHELL) \
								 $(top_srcdir)/build-aux/tap-driver.sh
PY_LOG_DRIVER = env AM_TAP_AWK='$(AWK)' $(SHELL) \
								 $(top_srcdir)/build-aux/tap-driver.sh
AM_PY_LOG_FLAGS = \
		--scriptlet-shell $(SCRIPTLET_SHELL) \
		--ldconfig $(LDCONFIG) \
		--bindir $(top_builddir)/src/pacman \
		--bindir $(top_builddir)/scripts
if !HAVE_LIBGPGME
AM_PY_LOG_FLAGS += --without-gpg
endif
if !HAVE_LIBCURL
AM_PY_LOG_FLAGS += --without-curl
endif

# create the pacman DB, cache, makepkg-template and system hook directories upon install
install-data-local:

update-po:

update-copyright:
	for file in $(shell sh -c 'git grep -l "Copyright .* Pacman Development" | grep -v "\.po"'); do \
	  sed -i -e "/Copyright (/s/-$(OLD)/-$(NEW)/" -e "/Copyright (/s/ $(OLD)/ $(OLD)-$(NEW)/" "$$file"; \
	done

.PHONY: update-po update-copyright
