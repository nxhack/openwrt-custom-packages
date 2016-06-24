#
# Copyright (c) 2016 Dog Hunter AG. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ajtcl-services
PKG_VERSION:=16.04
PKG_RELEASE:=1

PKG_SOURCE:=base_tcl-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.allseenalliance.org/cgit/services/base_tcl.git/snapshot/
PKG_MD5SUM:=3dfc63f9b256f5ed7b8d3a47d90f68b5

PKG_BUILD_DIR:=$(BUILD_DIR)/base_tcl-$(PKG_VERSION)

# SCons supports parallel builds but does not support make's jobserver
PKG_BUILD_PARALLEL:=$(if $(CONFIG_PKG_BUILD_USE_JOBSERVER),0,1)

PKG_CONFIG_DEPENDS:= \
	CONFIG_DEBUG

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/scons.mk

define Package/$(PKG_NAME)/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=ajtcl
  TITLE:=AllJoyn Thin Client Base Services library
  URL:=http://www.allseenalliance.org
  MAINTAINER:=AllSeen Alliance <allseen-core@lists.allseenalliance.org>
endef

define Package/$(PKG_NAME)
$(call Package/$(PKG_NAME)/Default)
  TITLE:=AllJoyn Thin Client - Base Services
  MENU:=0
endef

define Package/$(PKG_NAME)/description
	AllJoyn Thin Client Base Services is the standard AllJoyn services libraries for
	the AllJoyn Thin Client C library for developing ad hoc peer-to-peer
	applications that use the AllJoyn protocol. Revision : 7b875c76cb29304f955c5b5a4bafb2194c6f779e
endef

#define Package/$(PKG_NAME)-samples
#$(call Package/$(PKG_NAME)/Default)
#  TITLE:=AllJoyn Thin Client - Base Services - testing samples
#  DEPENDS:=ajtcl
#endef

#define Package/$(PKG_NAME)-samples/description
#Alljoyn Thin Client Base Services samples.  (This is primarily for testing.)
#endef

ifeq ($(CONFIG_DEBUG),y)
  ALLJOYN_BUILD_VARIANT:=debug
else
  ALLJOYN_BUILD_VARIANT:=release
endif

define Build/Configure/Default
	# Override default to do nothing
endef

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/ajtcl

define Build/Compile
	$(SCONS_VARS) \
	CROSS_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(FPIC) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	CROSS_LINKFLAGS="$(TARGET_LINKFLAGS) $(TARGET_LDFLAGS)" \
	CROSS_PATH=$(TARGET_PATH) \
	CROSS_PREFIX=$(TARGET_CC:gcc=) \
	scons -C $(PKG_BUILD_DIR) \
		$(PKG_JOBS) \
		WS=off \
		TARG=linux \
		"VARIANT=$(ALLJOYN_BUILD_VARIANT)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/include/ajtcl
	$(CP) $(PKG_BUILD_DIR)/dist/include/ajtcl/* $(1)/usr/include/ajtcl
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/dist/lib/* $(1)/usr/lib/
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/dist/lib/libajtcl_services.so $(1)/usr/lib/
endef

#define Package/$(PKG_NAME)-samples/install
#	$(INSTALL_DIR) $(1)/usr/bin
#endef

$(eval $(call BuildPackage,$(PKG_NAME)))
#$(eval $(call BuildPackage,$(PKG_NAME)-samples))
