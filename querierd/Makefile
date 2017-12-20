# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=querierd
PKG_VERSION:=0.2
PKG_RELEASE:=1
PKG_BRANCH:=afa077c36c02

PKG_SOURCE:=$(PKG_BRANCH).zip
PKG_SOURCE_URL:=https://bitbucket.org/marc_culler/querierd/get/
PKG_SOURCE_SUBDIR:=marc_culler-querierd-$(PKG_BRANCH)
PKG_HASH:=dba4f0605ab83be330bda6c19683287ed21fac9d7f2be6bbdfcbd237bea9a8f0

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/querierd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=IGMP querier service
  URL:=https://bitbucket.org/marc_culler/querierd
  DEPENDS:=+python-light +python-netifaces
endef

define Package/querierd/description
The querierd daemon will participate in the querier election process,
so you can run querierd daemons on several devices on your network,
some of which may not be running all the time.
endef

define Build/Prepare
	$(PKG_UNPACK)
	(cd $(BUILD_DIR) && mv $(PKG_SOURCE_SUBDIR)/* $(PKG_BUILD_DIR)/ && \
	mv $(PKG_SOURCE_SUBDIR)/.??* $(PKG_BUILD_DIR)/ && rmdir $(PKG_SOURCE_SUBDIR))
	$(Build/Patch)
endef

define Package/querierd/install
	$(call PyPackage/querierd/install)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/querierd.init $(1)/etc/init.d/querierd
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/etc/querierd $(1)/etc/
endef

$(eval $(call PyPackage,querierd))
$(eval $(call BuildPackage,querierd))
