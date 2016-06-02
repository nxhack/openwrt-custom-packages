#
# Copyright (C) 2008-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mg
PKG_VERSION:=20160103
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://devio.us/~bcallah/mg
PKG_MD5SUM:=3fb248f78b08a7395b87b1b6e940dc7c

PKG_MAINTAINER:=
PKG_LICENSE:=ISC BSD
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk

define Package/mg
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncurses
  TITLE:=microscopic GNU Emacs-style editor portable
  URL:=http://devio.us/~bcallah/mg/
  SUBMENU:=Editors
endef

define Package/mg/description
	This program is intended to be a small, fast, and portable
	editor for people who can't (or don't want to) run real
	Emacs for one reason or another.  It is compatible with GNU
	because there shouldn't be any reason to learn more than
	one Emacs flavor.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		LIBS="-lncurses" \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) \
		-D_GNU_SOURCE -D__dead='__attribute__((__noreturn__))' \
		-Dst_mtimespec=st_mtim -DNO_THEO" \
		CC="$(TARGET_CC)"
endef

define Package/mg/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mg))
