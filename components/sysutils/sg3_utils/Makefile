#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2012, Oracle and/or its affiliates. All rights reserved.
#

PREFERRED_BITS=64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= sg3_utils
COMPONENT_VERSION= 1.44
COMPONENT_FMRI= system/storage/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION= Applications/System Utilities
COMPONENT_PROJECT_URL= http://sg.danny.cz/sg/sg3_utils.html
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tgz
COMPONENT_ARCHIVE_HASH= sha256:8dae684d22e71b11353a48b16c95597af90f0cbe9bbd57f98d7f5544da5cae7b
COMPONENT_ARCHIVE_URL= http://sg.danny.cz/sg/p/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE= GPLv2+ and BSD 
COMPONENT_SUMMARY= Utilities for devices that use SCSI command sets

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

CPPFLAGS += -I$(COMPONENT_DIR)/$(COMPONENT_SRC)/include
CFLAGS += -std=c99 $(CPP_XPG6MODE)

CONFIGURE_OPTIONS +=	--disable-static
CONFIGURE_OPTIONS += CPPFLAGS="$(CPPFLAGS)"
CONFIGURE_OPTIONS += CFLAGS="$(CFLAGS)"

# Don't use rpath!
COMPONENT_POST_CONFIGURE_ACTION = \
	(cd $(BUILD_DIR_64) ; \
	$(GSED) -i 's|^hardcode_libdir_flag_spec=.*|hardcode_libdir_flag_spec=""|g' libtool ; \
	$(GSED) -i 's|^runpath_var=LD_RUN_PATH|runpath_var=DIE_RPATH_DIE|g' libtool)

PKG_PROTO_DIRS +=	$(COMPONENT_DIR)/files

# common targets
build:          $(BUILD_64)

install:        $(INSTALL_64)

test:           $(TEST_64)

REQUIRED_PACKAGES += shell/bash
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
