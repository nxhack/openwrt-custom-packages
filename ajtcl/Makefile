#
# Copyright (c) 2016 Dog Hunter AG. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ajtcl
PKG_VERSION:=16.04
PKG_RELEASE:=1

PKG_SOURCE:=ajtcl-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.allseenalliance.org/cgit/core/ajtcl.git/snapshot/
PKG_MD5SUM:=fa36257188701d0698065e5db9ca67ff

PKG_BUILD_DIR:=$(BUILD_DIR)/ajtcl-$(PKG_VERSION)

# SCons supports parallel builds but does not support make's jobserver
PKG_BUILD_PARALLEL:=$(if $(CONFIG_PKG_BUILD_USE_JOBSERVER),0,1)

PKG_CONFIG_DEPENDS:= \
	CONFIG_DEBUG

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk

define Package/ajtcl/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libpthread +librt
  URL:=http://www.allseenalliance.org
  TITLE:=The AllJoyn Thin Client Library
  MAINTAINER:=AllSeen Alliance <allseen-core@lists.allseenalliance.org>
endef

define Package/ajtcl
$(call Package/ajtcl/Default)
  TITLE:=AllJoyn Thin Client Library
  MENU:=1
endef

define Package/ajtcl/description
	AllJoyn Thin Client Library is a basic, low-level C library for developing
	ad hoc peer-to-peer applications that use the AllJoyn protocol. Revision : c7246570b10c70913c2b983b5f9353672908f73d
endef

define Package/ajtcl-samples
$(call Package/ajtcl/Default)
  TITLE:=AllJoyn Thin Client Library - testing samples
  DEPENDS:=ajtcl
endef

define Package/ajtcl-samples/description
	Alljoyn Thin Client Library samples.  (This is primarily for testing.)
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
	$(CP) $(PKG_BUILD_DIR)/dist/include/ajtcl/* $(1)/usr/include/ajtcl/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/dist/lib/* $(1)/usr/lib/
endef

define Package/ajtcl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/dist/lib/libajtcl.so $(1)/usr/lib/
endef

define Package/ajtcl-samples/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/dist/bin/* $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dist/test/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,ajtcl))
$(eval $(call BuildPackage,ajtcl-samples))
