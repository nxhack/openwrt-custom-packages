# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=querierd
PKG_VERSION:=0.2
PKG_RELEASE:=9

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/culler/querierd.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=ba1a1f1d9b38b4ccf72df1cc38f19a6c2c5665b8
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=4274ba2636c4420913eb5bb2e890fc75a4bdb6622385d6b65537ca2ac1822ec9

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

include ../../packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include ../../packages/lang/python/python3-package.mk

define Package/querierd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=IGMP querier service
  URL:=https://marc-culler.info/software/
  DEPENDS:=+python3-light +python3-netifaces
endef

define Package/querierd/description
The querierd daemon will participate in the querier election process,
so you can run querierd daemons on several devices on your network,
some of which may not be running all the time.
endef

define Package/querierd/install
	$(INSTALL_DIR) $(1)$(PYTHON3_PKG_DIR)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(CP) $(PKG_INSTALL_DIR)$(PYTHON3_PKG_DIR)/* \
		$(1)$(PYTHON3_PKG_DIR)/
	$(INSTALL_BIN) ./files/querierd.init $(1)/etc/init.d/querierd
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/etc/querierd $(1)/etc/
endef

$(eval $(call BuildPackage,querierd))
