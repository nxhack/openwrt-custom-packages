# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=RPi.GPIO
PKG_VERSION:=0.7.0
PKG_RELEASE:=1

PYPI_NAME:=RPi.GPIO
PKG_HASH:=7424bc6c205466764f30f666c18187a0824077daf20b295c42f08aea2cb87d3f

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENCE.txt
PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

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

$(eval $(call PyPackage,python-RPi.GPIO))
$(eval $(call BuildPackage,python-RPi.GPIO))
#$(eval $(call BuildPackage,python-RPi.GPIO-src))
$(eval $(call Py3Package,python3-RPi.GPIO))
$(eval $(call BuildPackage,python3-RPi.GPIO))
#$(eval $(call BuildPackage,python3-RPi.GPIO-src))
