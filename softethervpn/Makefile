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

PKG_MAINTAINER:=
PKG_LICENSE:=Custom
PKG_LICENSE_FILES:=

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
	make -C $(PKG_BUILD_DIR) -f src/makefiles/linux_32bit.mak clean
	make -C $(PKG_BUILD_DIR) -f src/makefiles/linux_32bit.mak src/bin/BuiltHamcoreFiles/unix/hamcore.se2
	mv $(PKG_BUILD_DIR)/src/bin/BuiltHamcoreFiles/unix/hamcore.se2 $(PKG_BUILD_DIR)/src/bin/BuiltHamcoreFiles/unix/hamcore.se2.1

	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/authors.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/backup_dir_readme.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/DriverPackages/
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/empty.config
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/empty_sevpnclient.config
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/eula.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/install_src.dat
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/lang.config
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/languages.txt
#	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/legal.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/openvpn_readme.pdf
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/openvpn_readme.txt
#	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/openvpn_sample.ovpn
#	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/root_certs.dat
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/SOURCES_OF_BINARY_FILES.TXT
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/strtable_cn.stb
#	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/strtable_en.stb
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/strtable_ja.stb
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpn16.exe
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpninstall_cn.inf
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpninstall_en.inf
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpninstall_ja.inf
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpnweb_sample_cn.htm
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpnweb_sample_en.htm
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/vpnweb_sample_ja.htm
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/warning_cn.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/warning_en.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/warning_ja.txt
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/webui/
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/winpcap_installer.exe
	rm -fr $(PKG_BUILD_DIR)/src/bin/hamcore/winpcap_installer_win9x.exe

	make -C $(PKG_BUILD_DIR) -f src/makefiles/linux_32bit.mak clean
	mv $(PKG_BUILD_DIR)/src/bin/BuiltHamcoreFiles/unix/hamcore.se2.1 $(PKG_BUILD_DIR)/src/bin/BuiltHamcoreFiles/unix/hamcore.se2
	touch -d "`date -d 1day`" $(PKG_BUILD_DIR)/src/bin/BuiltHamcoreFiles/unix/hamcore.se2

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

$(eval $(call BuildPackage,softethervpn))
