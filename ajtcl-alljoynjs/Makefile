#
# Copyright (c) 2016 Dog Hunter AG. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ajtcl-alljoynjs
PKG_VERSION:=15.04
PKG_RELEASE:=1

PKG_SOURCE:=alljoyn-js-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.allseenalliance.org/cgit/core/alljoyn-js.git/snapshot/
PKG_MD5SUM:=276767da532bf845ca014c7a5d8f7885

# SCons supports parallel builds but does not support make's jobserver
PKG_BUILD_PARALLEL:=$(if $(CONFIG_PKG_BUILD_USE_JOBSERVER),0,1)

PKG_CONFIG_DEPENDS:= \
	CONFIG_DEBUG

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk

define Package/ajtcl-alljoynjs
  TITLE:=AllJoyn Thin Client - AllJoynJS
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=ajtcl +ajtcl-services +duktape
  URL:=http://www.allseenalliance.org
  MAINTAINER:=AllSeen Alliance <allseen-core@lists.allseenalliance.org>
  MENU:=1
endef

define Package/ajtcl-alljoynjs/description
	AllJoyn Thin Client AllJoynJS binding is a basic, low-level JavaScript
	interpreter that uses the Duktape embeddable JavaScript engine for developing
	ad hoc peer-to-peer applications that use the AllJoyn protocol. MASTER Revision
endef

define Package/ajtcl-alljoynjs-samples
$(call Package/ajtcl-alljoynjs)
  TITLE+=- testing samples
  DEPENDS:=ajtcl-alljoynjs
  MENU:=0
endef

define Package/ajtcl-alljoynjs-samples/description
	Sample JavaScript programs that use AllJoyn via alljoyn.js.
endef

ifeq ($(CONFIG_DEBUG),y)
  ALLJOYN_BUILD_VARIANT:=debug
else
  ALLJOYN_BUILD_VARIANT:=release
endif

define Build/Configure/Default
	# Override default to do nothing
endef

define Build/Compile
	YUN_BUILD=0 \
	CROSS_CFLAGS="-I$(STAGING_DIR)/usr/src/duktape/src -I$(STAGING_DIR)/usr/include/ajtcl $(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(TARGET_CPPFLAGS)" \
	CROSS_LINKFLAGS="$(TARGET_LINKFLAGS) $(TARGET_LDFLAGS) -lajtcl_services" \
	CROSS_PATH=$(TARGET_PATH) \
	CROSS_PREFIX=$(REAL_GNU_TARGET_NAME)- \
	DUKTAPE_DIST="$(STAGING_DIR)/usr/src/duktape" \
	scons -C $(PKG_INSTALL_DIR) \
		$(PKG_JOBS) \
		WS=off \
		TARG=linux \
		"VARIANT=$(ALLJOYN_BUILD_VARIANT)"
endef

define Package/ajtcl-alljoynjs/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/alljoynjs $(1)/usr/bin/
endef

define Package/ajtcl-alljoynjs-samples/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DIR) $(1)/usr/share/alljoyn.js
	$(CP) $(PKG_INSTALL_DIR)/js/*.js $(1)/usr/share/alljoyn.js/
endef

$(eval $(call BuildPackage,ajtcl-alljoynjs))
$(eval $(call BuildPackage,ajtcl-alljoynjs-samples))
