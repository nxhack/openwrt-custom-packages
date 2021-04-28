#
# Copyright (C) 2015-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmraa
PKG_VERSION:=2.2.0
PKG_RELEASE:=4

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=https://codeload.github.com/eclipse/mraa/tar.gz/v$(PKG_VERSION)?
#PKG_HASH:=076669bee8423ffef3065735b293a329020be86630fea457174dbfcc67a0554a
#PKG_BUILD_DIR:=$(BUILD_DIR)/mraa-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/eclipse/mraa.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=833bac569c5fae2905fd6f6abc90c86c784b904c
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=a63e03a1b4c96c54ad0bd5f4ae627b2c288ca645045a671faa6ea049c8180a40

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>, Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DEPENDS:=swig/host node/host PACKAGE_node:node
CMAKE_INSTALL:=1
PKG_USE_MIPS16:=0
PYTHON3_PKG_BUILD:=0

include $(INCLUDE_DIR)/package.mk
#include ../../packages/devel/ninja/ninja-cmake.mk
include $(INCLUDE_DIR)/cmake.mk
include ../../packages/lang/python/python3-package.mk

CMAKE_OPTIONS += \
	-DENABLEEXAMPLES=0 \
	-DBUILDSWIGNODE=$(if $(CONFIG_PACKAGE_libmraa-node),ON,OFF) \
	-DSWIG_EXECUTABLE=$(STAGING_DIR_HOSTPKG)/bin/swig \
	-DSWIG_DIR=$(STAGING_DIR_HOSTPKG)/share/swig/4.1.0 \
	-DFIRMATA=ON

define Package/libmraa/Default
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=IoT
  TITLE:=Eclipse MRAA lowlevel IO library
  URL:=https://projects.eclipse.org/projects/iot.mraa
endef

define Package/libmraa/Default/description
  Libmraa is a C/C++ library with bindings to Java, Python and JavaScript to interface
with the IO on Galileo, Edison & other platforms, with a structured and sane API where
port names/numbering matches the board that you are on. Use of libmraa does not tie you
to specific hardware with board detection done at runtime you can create portable code
that will work across the supported platforms.
endef

define Package/libmraa
  $(call Package/libmraa/Default)
  TITLE:=Eclipse MRAA lowlevel IO C/C++ library
  DEPENDS:=+libstdcpp +libjson-c @!arc @!armeb @!powerpc
endef

define Package/libmraa/description
$(call Package/libmraa/Default/description)

This package contains the C/C++ libraries.
endef

define Package/libmraa-node
  $(call Package/libmraa/Default)
  TITLE:=Eclipse MRAA lowlevel IO Node.js library
  DEPENDS:=+libmraa @PACKAGE_node
endef

define Package/libmraa-node/description
$(call Package/libmraa/Default/description)

This package contains the Node.js libraries.
endef

define Package/libmraa-python3
  $(call Package/libmraa/Default)
  TITLE:=Eclipse MRAA lowlevel IO Python3 library
  DEPENDS:=+libmraa +python3-light
endef

define Package/libmraa-python3/description
$(call Package/libmraa/Default/description)

This package contains the Python3 libraries.
endef

define Package/libmraa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmraa.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mraa-* $(1)/usr/bin/
endef

define Package/libmraa-node/install
	$(INSTALL_DIR) $(1)/usr/lib/node/mraa
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/mraa/* $(1)/usr/lib/node/mraa/
endef

define Package/libmraa-python3/install
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON3_VERSION)/site-packages
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/python$(PYTHON3_VERSION)/site-packages/* \
		$(1)/usr/lib/python$(PYTHON3_VERSION)/site-packages/
endef

$(eval $(call BuildPackage,libmraa))
$(eval $(call BuildPackage,libmraa-node))
$(eval $(call BuildPackage,libmraa-python3))
