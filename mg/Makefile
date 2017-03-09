#
# Copyright (C) 2008-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mg
PKG_VERSION:=20161016
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://devio.us/~bcallah/mg/
PKG_MD5SUM:=5ca187eba256d43ddd7a4299dde030c1
PKG_HASH:=bcb4be59aaa30ae8dd0e9aed3c0a5ff8bf2dae6e6768396d37c11aaaab29d370

PKG_LICENSE:=PUBLICDOMAIN ISC BSD VARIOUS
PKG_LICENSE_FILES:=README.md

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/mg
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncurses
  TITLE:=Small Emacs-like editor from OpenBSD
  URL:=https://devio.us/~bcallah/mg/
  SUBMENU:=Editors
endef

define Package/mg/description
 Mg is intended to be a small, fast, and portable editor for people who
 can't (or don't want to) run emacs for one reason or another, or are not
 familiar with the vi editor. It is compatible with emacs because there
 shouldn't be any reason to learn more editor types than emacs or vi.
endef

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		LIBS="-lncurses" \
		CFLAGS="$(TARGET_CFLAGS) \
			-D_GNU_SOURCE -D__dead='__attribute__((__noreturn__))' \
			-Dst_mtimespec=st_mtim -DNO_THEO" \
		CC="$(TARGET_CC)"
endef

define Package/mg/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mg $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mg))
