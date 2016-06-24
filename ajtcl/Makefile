#
# Copyright (c) 2016 Dog Hunter AG. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ajtcl
PKG_VERSION:=15.04b
PKG_RELEASE:=1

PKG_SOURCE:=ajtcl-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.allseenalliance.org/cgit/core/ajtcl.git/snapshot/
PKG_MD5SUM:=44c61bff40b4114077ffa04d49c820c6

PKG_BUILD_DIR:=$(BUILD_DIR)/ajtcl-$(PKG_VERSION)

# SCons supports parallel builds but does not support make's jobserver
PKG_BUILD_PARALLEL:=$(if $(CONFIG_PKG_BUILD_USE_JOBSERVER),0,1)

PKG_CONFIG_DEPENDS:= \
	CONFIG_DEBUG

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/scons.mk

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
  DEPENDS:=+ajtcl
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
	$(SCONS_VARS) \
	CROSS_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS) $(FPIC) $(TARGET_CPPFLAGS) $(EXTRA_CPPFLAGS)" \
	CROSS_LINKFLAGS="$(TARGET_LINKFLAGS) $(TARGET_LDFLAGS)" \
	CROSS_PATH=$(TARGET_PATH) \
	CROSS_PREFIX=$(TARGET_CC:gcc=) \
	scons -C $(PKG_BUILD_DIR) \
		$(PKG_JOBS) \
		TARG=linux \
		BR=off \
		ICE=off \
		POLICYDB=on \
		WS=off \
		"VARIANT=$(ALLJOYN_BUILD_VARIANT)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/include/ajtcl
	$(CP) $(PKG_BUILD_DIR)/inc/*.h $(1)/usr/include/ajtcl/
	$(CP) $(PKG_BUILD_DIR)/target/linux/*.h $(1)/usr/include/ajtcl/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libajtcl_st.a $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libajtcl.so $(1)/usr/lib/
endef

define Package/ajtcl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libajtcl.so $(1)/usr/lib/
endef

define Package/ajtcl-samples/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/secure/SecureClient $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/secure/SecureService $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/basic/basic_service $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/basic/basic_client $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/basic/signal_service $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/basic/nameChange_client $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/samples/basic/signalConsumer_client $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/mutter $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/ajlite $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/aestest $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/aesbench $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/svclite $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/clientlite $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/siglite $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/sessions $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/nvramtest $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/test/bastress2 $(1)/usr/bin/
endef

$(eval $(call BuildPackage,ajtcl))
$(eval $(call BuildPackage,ajtcl-samples))
