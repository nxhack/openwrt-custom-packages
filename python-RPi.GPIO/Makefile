# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=RPi.GPIO
PKG_VERSION:=0.7.1
PKG_RELEASE:=1

PYPI_NAME:=RPi.GPIO
PKG_HASH:=cd61c4b03c37b62bba4a5acfea9862749c33c618e0295e7e90aa4713fb373b70

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENCE.txt
PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

PYTHON3_PKG_SETUP_ARGS:=

define Package/python3-RPi.GPIO
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  URL:=https://sourceforge.net/projects/raspberry-gpio-python/
  TITLE:=python3-RPi.GPIO
  DEPENDS:=+PACKAGE_python3-RPi.GPIO:python3-light
  VARIANT:=python3
endef

define Package/python3-RPi.GPIO/description
 A module to control Raspberry Pi GPIO channels
.
(Variant for Python3)
endef

$(eval $(call Py3Package,python3-RPi.GPIO))
$(eval $(call BuildPackage,python3-RPi.GPIO))
#$(eval $(call BuildPackage,python3-RPi.GPIO-src))
