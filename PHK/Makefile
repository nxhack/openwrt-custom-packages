# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=PHK
PKG_VERSION:=1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/nxhack/Personal-HomeKit-HAP/tar.gz/$(PKG_VERSION)?
PKG_HASH:=407f34d55ddc75594afb0abbf502a718f3d89a1c65f4657782043dea045fe4d2
PKG_BUILD_DIR:=$(BUILD_DIR)/Personal-HomeKit-HAP-$(PKG_VERSION)

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=License

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/PHK
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=PHK -- prints a snarky message
  URL:=https://github.com/etwmc/Personal-HomeKit-HAP
  DEPENDS:=+libavahi-compat-libdnssd +libopenssl +libstdcpp
endef

define Package/PHK/description
 This project will provide source code to build a HomeKit support accessories.
endef

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/avahi-compat-libdns_sd
TARGET_LDFLAGS+=-lcrypto -lssl

define Package/PHK/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/PHK $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,PHK))
