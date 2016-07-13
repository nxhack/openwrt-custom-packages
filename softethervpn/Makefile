#
# Copyright (c) 2016 LEDE Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=softethervpn
PKG_VERSION:=4.21-9613
#PKG_VERSION2:=rtm
PKG_VERSION2:=beta
PKG_DATE:=2016.04.24
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-v$(PKG_VERSION)
PKG_SOURCE:=softether-src-v$(PKG_VERSION)-$(PKG_VERSION2).tar.gz
PKG_SOURCE_URL:=http://jp.softether-download.com/files/softether/v$(PKG_VERSION)-$(PKG_VERSION2)-$(PKG_DATE)-tree/Source_Code/
PKG_MD5SUM:=928d882d5fc23e00f0a5fa4ebf292ab9

PKG_BUILD_DEPENDS:=softethervpn/host

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/softethervpn
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  DEPENDS:=+libopenssl +libpthread +librt +libreadline
  URL:=http://www.softether.org/
  TITLE:=An Open-Source Free​Cross-platform Multi-protocol VPN Program
endef

define Package/softethervpn/description
 SoftEther VPN ("SoftEther" means "Software Ethernet") is one of the world's most powerful and easy-to-use multi-protocol VPN software. It runs on Windows, Linux, Mac, FreeBSD and Solaris.
endef

define Package/softethervpn/conffiles
	/usr/bin/vpn_bridge.config
	/usr/bin/vpn_client.config
	/usr/bin/vpn_server.config
endef

define Build/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 1
	$(Build/Patch)
endef

define Build/Configure
endef

ifeq ($(ARCH),mips)
	SE4WRT_OPTIONS := -minterlink-mips16
endif
ifeq ($(ARCH),mipsel)
	SE4WRT_OPTIONS := -minterlink-mips16
endif

define Build/Compile
	$(MAKE) \
		$(TARGET_CONFIGURE_OPTS) \
		CCFLAGS="-I$(STAGING_DIR)/usr/include $(ICONV_CFLAGS) $(SE4WRT_OPTIONS)" \
		LDFLAGS="-L$(STAGING_DIR)/usr/lib $(ICONV_LDFLAGS) -liconv" \
		-C $(PKG_BUILD_DIR) \
		-f src/makefiles/linux_32bit.mak
endef

define Package/softethervpn/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/vpnserver/* $(1)/usr/bin
	ln -s vpnserver $(1)/usr/bin/vpnclient
	ln -s vpnserver $(1)/usr/bin/vpnbridge
	ln -s vpnserver $(1)/usr/bin/vpncmd
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rc/vpnserver $(1)/etc/init.d/softethervpnserver
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rc/vpnclient $(1)/etc/init.d/softethervpnclient
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rc/vpnbridge $(1)/etc/init.d/softethervpnbridge
endef

define Host/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(HOST_BUILD_DIR) --strip-components 1
endef

define Host/Compile
	$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)/src/Mayaqua \
		$(HOST_MAKE_FLAGS)
	$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)/src/Cedar \
		$(HOST_MAKE_FLAGS)
	$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)/src/hamcorebuilder \
		$(HOST_MAKE_FLAGS)
endef

define Host/Install
	$(INSTALL) -m 0755 $(HOST_BUILD_DIR)/src/hamcorebuilder/hamcorebuilder $(STAGING_DIR)/host/bin/hamcorebuilder
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,softethervpn))
