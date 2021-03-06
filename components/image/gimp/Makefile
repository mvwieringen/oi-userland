#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2017 Alexander Pyhalov
# Copyright (c) 2019 Tim Mooney
#

BUILD_BITS= 64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gimp
COMPONENT_VERSION=	2.10.20
COMPONENT_PROJECT_URL=	https://www.gimp.org/
COMPONENT_SUMMARY=	Gimp - The Free & Open Source Image Editor
COMPONENT_FMRI=		image/editor/gimp
COMPONENT_CLASSIFICATION=	Applications/Graphics and Imaging
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:e12f9f874b1a007c4277b60aa81e0b67330be7e6153e5749ead839b902fc7b3c
COMPONENT_ARCHIVE_URL=	https://download.gimp.org/pub/gimp/v2.10/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	GPLv3
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

CFLAGS += -I/usr/include/glib-2.0 -I/usr/lib/$(MACH64)/glib-2.0/include
CFLAGS += -I/usr/include/libmng

# build with the distribution preferred libjpeg implementation
CFLAGS   += $(JPEG_CPPFLAGS) $(JPEG_CFLAGS)
CXXFLAGS += $(JPEG_CPPFLAGS) $(JPEG_CXXFLAGS)
LDFLAGS  += $(JPEG_LDFLAGS)

COMPONENT_PREP_ACTION =	( cd $(@D)  && \
				libtoolize --force &&\
				intltoolize --force --copy --automake &&\
				aclocal -I. &&\
				automake -a -c -f &&\
				autoconf)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=$(CONFIGURE_LIBDIR.$(BITS))
CONFIGURE_OPTIONS+=	--localstatedir=/var/lib
CONFIGURE_OPTIONS+=	--enable-mp
CONFIGURE_OPTIONS+=	--enable-default-binary
CONFIGURE_OPTIONS+=	--enable-mmx=no
CONFIGURE_OPTIONS+=	--with-lcms=2

CONFIGURE_ENV+= PYTHON=$(PYTHON)

# Tests need this
unexport SHELLOPTS

# Replace "#!/usr/bin/env ..." shebang lines with properly versioned ones.
COMPONENT_POST_INSTALL_ACTION = \
        /usr/bin/find $(PROTO_DIR) -name *.py \
                -exec $(GSED) -i -e '1s|env python.*|$(MACH64)/python$(PYTHON_VERSION)|' "{}" \; ;

# Build dependencies
REQUIRED_PACKAGES += library/mypaint-brushes
REQUIRED_PACKAGES += library/python/pygobject
REQUIRED_PACKAGES += library/python/pygtk2

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += compress/bzip2
REQUIRED_PACKAGES += compress/xz
REQUIRED_PACKAGES += image/library/babl
REQUIRED_PACKAGES += image/library/gegl
REQUIRED_PACKAGES += image/library/gexiv2
REQUIRED_PACKAGES += image/library/libjpeg8-turbo
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += image/library/librsvg
REQUIRED_PACKAGES += image/library/libtiff
REQUIRED_PACKAGES += image/library/openjpeg
REQUIRED_PACKAGES += library/aalib
REQUIRED_PACKAGES += library/c++/harfbuzz
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk2
REQUIRED_PACKAGES += library/desktop/json-glib
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/graphics/libmng
REQUIRED_PACKAGES += library/ilmbase
REQUIRED_PACKAGES += library/lcms2
REQUIRED_PACKAGES += library/libmypaint
REQUIRED_PACKAGES += library/libpoppler
REQUIRED_PACKAGES += library/libwebp
REQUIRED_PACKAGES += library/openexr
REQUIRED_PACKAGES += library/python/pygobject-27
REQUIRED_PACKAGES += library/python/pygtk2-27
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += print/filter/ghostscript
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxcursor
REQUIRED_PACKAGES += x11/library/libxext
REQUIRED_PACKAGES += x11/library/libxfixes
REQUIRED_PACKAGES += x11/library/libxmu
REQUIRED_PACKAGES += x11/library/libxpm
