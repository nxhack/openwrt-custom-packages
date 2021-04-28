#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=swig
PKG_VERSION:=4.0.2
PKG_RELEASE:=3

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=@SF/$(PKG_NAME)
#PKG_HASH:=d53be9730d8d58a16bf0cbd1f8ac0c0c3e1090573168bfa151b01eb47fa906fc

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/swig/swig.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=429288fa1c753dcb2d34f363e51c3b924ac173bb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=fbe85c489f4b833e58c88e2e1f2d3e762f01a6d25e28ff99a1db5fbbdc31999e

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>, Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

PKG_HOST_ONLY:=1
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/swig
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=swig binding generator
  URL:=http://swig.org/
  BUILDONLY:=1
endef

HOST_CONFIGURE_ARGS += \
	--disable-ccache \
	--without-pcre

define Package/swig/description
  tool that generates bindings for various languages
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,swig))
