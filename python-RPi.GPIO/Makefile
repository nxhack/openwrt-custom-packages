# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=RPi.GPIO
PKG_VERSION:=0.6.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/af/2f/407b6e4cc8a0bdf434825a160bba1807991886b63cce16a5f1a6e1f24cdf
PKG_HASH:=a4210ad63bfe844e43995286de0d3950dfacfa0f3799bb9392770ac54a7d2e47

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENCE.txt
PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(BUILD_VARIANT)-$(PKG_NAME)-$(PKG_VERSION)

OW_VER:=$(shell git --git-dir=$(TOPDIR)/.git describe --abbrev=0 --always --tag)
ifneq ($(filter reboot v18.06%, $(OW_VER)),)
  IS_HEAD:=y
endif

ifneq ($(IS_HEAD),y)
PKG_BUILD_DEPENDS:=PACKAGE_python-RPi.GPIO:python \
                   PACKAGE_python-RPi.GPIO:python-setuptools \
                   PACKAGE_python3-RPi.GPIO:python \
                   PACKAGE_python3-RPi.GPIO:python3-setuptools
endif

include $(INCLUDE_DIR)/package.mk
ifeq ($(IS_HEAD),y)
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk
else
$(call include_mk, python-package.mk)
$(call include_mk, python3-package.mk)
endif

PKG_UNPACK:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

define Package/python-RPi.GPIO/Default
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  URL:=https://sourceforge.net/projects/raspberry-gpio-python/
endef

define Package/python-RPi.GPIO
$(call Package/python-RPi.GPIO/Default)
  TITLE:=python-RPi.GPIO
  DEPENDS:=+PACKAGE_python-RPi.GPIO:python-light
  VARIANT:=python
endef

define Package/python3-RPi.GPIO
$(call Package/python-RPi.GPIO/Default)
  TITLE:=python3-RPi.GPIO
  DEPENDS:=+PACKAGE_python3-RPi.GPIO:python3-light
  VARIANT:=python3
endef

define Package/python-RPi.GPIO/description
 A module to control Raspberry Pi GPIO channels
endef

define Package/python3-RPi.GPIO/description
$(call Package/python-RPi.GPIO/description)
.
(Variant for Python3)
endef

PYTHON_PKG_SETUP_ARGS:=
PYTHON3_PKG_SETUP_ARGS:=

$(eval $(call PyPackage,python-RPi.GPIO))
$(eval $(call BuildPackage,python-RPi.GPIO))
#$(eval $(call BuildPackage,python-RPi.GPIO-src))
$(eval $(call Py3Package,python3-RPi.GPIO))
$(eval $(call BuildPackage,python3-RPi.GPIO))
#$(eval $(call BuildPackage,python3-RPi.GPIO-src))
