#
# Copyright (C) Dog Hunter AG 2014-2016
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=duktape
PKG_VERSION:=1.5.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://duktape.org/
PKG_MD5SUM:=6fa1783b2eddaab4ab815cd894624fba

PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt

include $(INCLUDE_DIR)/package.mk

define Package/duktape
  SECTION:=lang
  CATEGORY:=Languages
  DEPENDS:=+libstdcpp +libc +libpthread
  TITLE:=Duktape embeddable JavaScript interpreter
  URL:=http://www.duktape.org
endef

define Package/duktape/description
  Duktape is a light-weight embeddable JavaScript interpreter.  It is provided as a C source file that is to be compiled into other projects.  Because it is highly configurable at compile-time, it is not suitable for being built as a library.
endef

define Build/Configure
endef

define Build/Compile
	CC=$(TARGET_CC) \
	CCOPTS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(TARGET_LINKFLAGS) $(TARGET_LDFLAGS)" \
	$(MAKE) -f $(PKG_BUILD_DIR)/Makefile.cmdline -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/src
	$(INSTALL_DIR) $(1)/usr/src/duktape
	$(INSTALL_DIR) $(1)/usr/src/duktape/src
	$(CP) $(PKG_BUILD_DIR)/src/*.c $(1)/usr/src/duktape/src
	$(CP) $(PKG_BUILD_DIR)/src/*.h $(1)/usr/src/duktape/src
endef

define Package/duktape/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/duk $(1)/usr/bin/
endef

$(eval $(call BuildPackage,duktape))
