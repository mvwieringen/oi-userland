# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2018 Alexander Pyhalov
#

BUILD_STYLE = setup.py
BUILD_BITS = NO_ARCH
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		chardet
COMPONENT_VERSION=	3.0.4
COMPONENT_REVISION=	3
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:84ab92ed1c4d4f16916e05906b6b75a6c0fb5db821cc65e70cbd64a3e2a5eaae
COMPONENT_ARCHIVE_URL=	$(call pypi_url)
COMPONENT_PROJECT_URL=	https://github.com/chardet/chardet

PYTHON_VERSIONS=	2.7 3.5

TEST_TARGET=		$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

COMPONENT_POST_INSTALL_ACTION = \
        (cd $(PROTO_DIR)/usr/bin ; \
                $(MV) chardetect chardetect-$(PYTHON_VERSION); )

# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/setuptools-27
REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-35
