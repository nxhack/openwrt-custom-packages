# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=v2ray-plugin
PKG_VERSION:=1.3.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/shadowsocks/v2ray-plugin/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=0ffb0a938bae58ea40a024cb04418c7fecb74f7d807de27ae0589c42307802a4

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/shadowsocks/v2ray-plugin

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/v2ray-plugin
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  TITLE:=SIP003 plugin for shadowsocks, based on v2ray
  URL:=https://github.com/shadowsocks/v2ray-plugin
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/v2ray-plugin/description
 Yet another SIP003 plugin for shadowsocks, based on v2ray
endef

define PyPackage/v2ray-plugin/install
	$(call GoPackage/Package/Install/Bin,$(1))
endef

$(eval $(call GoBinPackage,v2ray-plugin))
$(eval $(call BuildPackage,v2ray-plugin))
