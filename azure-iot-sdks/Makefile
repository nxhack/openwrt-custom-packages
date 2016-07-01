#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=azure-iot-sdks
PKG_VERSION:=2016-06-17
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Azure/azure-iot-sdks.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=867fad9254f3fb633aed732b650c322795014b6c
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/azure-iot-sdks
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libopenssl +libuuid +libcurl +libpthread
  TITLE:=Azure IoT SDK
endef

define Package/azure-iot-sdks/description
  The Microsoft Azure IoT device SDKs contain code that facilitate building devices and applications that connect to and are managed by Azure IoT Hub services
endef

define Build/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 2 --wildcards *c
	$(Build/Patch)
	cp $(PKG_BUILD_DIR)/build_all/arduino/CMakeList.append $(PKG_BUILD_DIR)
endef

define Build/Configure
	IN_OPENWRT=1 \
	TARGET_CPPFLAGS="$(TARGET_CPPFLAGS)" \
	TARGET_CFLAGS="$(TARGET_CFLAGS) -DIN_OPENWRT" \
	TARGET_LDFLAGS="$(TARGET_LDFLAGS)" \
	AR="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)ar" \
	AS="$(TOOLCHAIN_DIR)/bin/$(TARGET_CC) -c $(TARGET_CFLAGS)" \
	LD="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)ld" \
	NM="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)nm" \
	CC="$(TOOLCHAIN_DIR)/bin/$(TARGET_CC)" \
	GCC="$(TOOLCHAIN_DIR)/bin/$(TARGET_CC)" \
	CXX="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)g++" \
	RANLIB="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)ranlib" \
	STRIP="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)strip" \
	OBJCOPY="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)objcopy" \
	OBJDUMP="$(TOOLCHAIN_DIR)/bin/$(TARGET_CROSS)objdump" \
	cmake -DCMAKE_FIND_ROOT_PATH="$(TOOLCHAIN_DIR)" $(PKG_BUILD_DIR)/CMakeLists.txt -DIN_OPENWRT=1 -Duse_amqp:bool=ON -Duse_http:bool=ON -Duse_mqtt:bool=OFF -Dskip_unittests:bool=ON -Duse_floats:bool=OFF -Duse_condition:bool=OFF
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/azure-iot-sdks
	$(CP) $(PKG_BUILD_DIR)/azure-c-shared-utility/inc/* $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/iothub_client/inc/* $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/serializer/inc/* $(STAGING_DIR)/usr/include/
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/azure-c-shared-utility/*.a $(STAGING_DIR)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/iothub_client/*.a $(STAGING_DIR)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/serializer/*.a $(STAGING_DIR)/usr/lib/
endef

define Package/azure-iot-sdks/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/azure-c-shared-utility/*.a $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/iothub_client/*.a $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/serializer/*.a $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/share/azure-iot-sdk/samples
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/serializer/samples/remote_monitoring/remote_monitoring $(1)/usr/share/azure-iot-sdk/samples/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/serializer/samples/simplesample_http/simplesample_http $(1)/usr/share/azure-iot-sdk/samples/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/serializer/samples/simplesample_amqp/simplesample_amqp $(1)/usr/share/azure-iot-sdk/samples/
endef

$(eval $(call BuildPackage,azure-iot-sdks))
