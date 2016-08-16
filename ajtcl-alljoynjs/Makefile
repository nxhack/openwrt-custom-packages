#
# Copyright (c) 2016 Dog Hunter AG. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ajtcl-alljoynjs
PKG_VERSION:=16.04
PKG_RELEASE:=1

PKG_SOURCE:=alljoyn-js-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.allseenalliance.org/cgit/core/alljoyn-js.git/snapshot/
PKG_MD5SUM:=68983d7aa23ce4da45a06dce95c21ad5

PKG_BUILD_DIR:=$(BUILD_DIR)/alljoyn-js-$(PKG_VERSION)

# SCons supports parallel builds but does not support make's jobserver
PKG_BUILD_PARALLEL:=$(if $(CONFIG_PKG_BUILD_USE_JOBSERVER),0,1)

PKG_CONFIG_DEPENDS:= \
	CONFIG_DEBUG

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/scons.mk

define Package/$(PKG_NAME)
  TITLE:=AllJoyn Thin Client - AllJoynJS
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+ajtcl +ajtcl-services +duktape
  URL:=http://www.allseenalliance.org
  MAINTAINER:=AllSeen Alliance <allseen-core@lists.allseenalliance.org>
  MENU:=1
endef

define Package/$(PKG_NAME)/description
	AllJoyn Thin Client AllJoynJS binding is a basic, low-level JavaScript
	interpreter that uses the Duktape embeddable JavaScript engine for developing
	ad hoc peer-to-peer applications that use the AllJoyn protocol. MASTER Revision
endef

define Package/$(PKG_NAME)-samples
$(call Package/$(PKG_NAME))
  TITLE+=- testing samples
  DEPENDS:=$(PKG_NAME)
  MENU:=0
endef

define Package/$(PKG_NAME)-samples/description
	Sample JavaScript programs that use AllJoyn via alljoyn.js.
endef

ifeq ($(CONFIG_DEBUG),y)
  ALLJOYN_BUILD_VARIANT:=debug
else
  ALLJOYN_BUILD_VARIANT:=release
endif

define Build/Configure
endef

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/src/duktape/src -I$(STAGING_DIR)/usr/include/ajtcl
TARGET_LDFLAGS+=-lajtcl -lajtcl_services_config -lajtcl_services

define Build/Compile
	YUN_BUILD=0 \
	$(SCONS_VARS) \
	CROSS_PREFIX=$(REAL_GNU_TARGET_NAME)- \
	CROSS_PATH=$(TARGET_PATH) \
	CROSS_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(FPIC) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	CROSS_LINKFLAGS="$(TARGET_LINKFLAGS) $(TARGET_LDFLAGS)" \
	DUKTAPE_DIST="$(STAGING_DIR)/usr/src/duktape" \
	scons -C $(PKG_BUILD_DIR) \
		prefix=/usr \
		$(SCONS_OPTIONS) \
		$(PKG_JOBS) \
		TARG=linux \
		BR=on \
		ICE=off \
		POLICYDB=on \
		WS=off \
		"TARGET_CC=$$(TARGET_CC)" \
		"TARGET_CXX=$$(TARGET_CXX)" \
		"TARGET_CFLAGS=$$(TARGET_CFLAGS)" \
		"TARGET_CPPFLAGS=$$(TARGET_CPPFLAGS)" \
		"TARGET_PATH=$$(TARGET_PATH)" \
		"TARGET_LINKFLAGS=$$(TARGET_LDFLAGS)" \
		"TARGET_LINK=$$(TARGET_CC)" \
		"TARGET_AR=$$(TARGET_AR)" \
		"TARGET_RANLIB=$$(TARGET_RANLIB)" \
		"STAGING_DIR=$$(STAGING_DIR)" \
		"VARIANT=$(ALLJOYN_BUILD_VARIANT)"
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/alljoynjs $(1)/usr/bin/
endef

define Package/$(PKG_NAME)-samples/install
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/usr/share
	$(INSTALL_DIR) $(1)/usr/share/alljoyn.js
	$(CP) $(PKG_BUILD_DIR)/js/*.js $(1)/usr/share/alljoyn.js/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
$(eval $(call BuildPackage,$(PKG_NAME)-samples))
