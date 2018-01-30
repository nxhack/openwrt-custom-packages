# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=netifaces
PKG_VERSION:=0.10.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pypi.python.org/packages/72/01/ba076082628901bca750bf53b322a8ff10c1d757dc29196a8e6082711c9d
PKG_HASH:=0c4da523f36d36f1ef92ee183f2512f3ceb9a9d2a45f7d19cda5a42c6689ebe0

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=README.rst
PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-$(PKG_NAME)-$(PKG_VERSION)

ifdef CONFIG_BUSYBOX_DEFAULT_NSLOOKUP_LEDE
PKG_BUILD_DEPENDS:=PACKAGE_python-netifaces:python \
                   PACKAGE_python-netifaces:python-setuptools \
                   PACKAGE_python3-netifaces:python \
                   PACKAGE_python3-netifaces:python3-setuptools
endif

include $(INCLUDE_DIR)/package.mk
ifdef CONFIG_BUSYBOX_DEFAULT_NSLOOKUP_LEDE
$(call include_mk, python-package.mk)
$(call include_mk, python3-package.mk)
else
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk
endif

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

define Package/python-netifaces/Default
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  URL:=https://bitbucket.org/al45tair/netifaces
endef

define Package/python-netifaces
$(call Package/python-netifaces/Default)
  TITLE:=python-netifaces
  DEPENDS:=+PACKAGE_python-netifaces:python-light
  VARIANT:=python
endef

define Package/python3-netifaces
$(call Package/python-netifaces/Default)
  TITLE:=python3-netifaces
  DEPENDS:=+PACKAGE_python3-netifaces:python3-light
  VARIANT:=python3
endef

define Package/python-netifaces/description
Portable network interface information.
endef

define Package/python3-netifaces/description
$(call Package/python-netifaces/description)
.
(Variant for Python3)
endef

$(eval $(call PyPackage,python-netifaces))
$(eval $(call BuildPackage,python-netifaces))
#$(eval $(call BuildPackage,python-netifaces-src))
$(eval $(call Py3Package,python3-netifaces))
$(eval $(call BuildPackage,python3-netifaces))
#$(eval $(call BuildPackage,python3-netifaces-src))
