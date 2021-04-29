#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=swig
PKG_VERSION:=4.1.0
PKG_RELEASE:=0

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=@SF/$(PKG_NAME)
#PKG_HASH:=d53be9730d8d58a16bf0cbd1f8ac0c0c3e1090573168bfa151b01eb47fa906fc

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/swig/swig.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=429288fa1c753dcb2d34f363e51c3b924ac173bb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=7b939b655f4a3b6d4532a58a817bed787a3971f370eb4812b8356e60a81c8a37

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>, Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=node/host node-gyp/host
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
	--with-jsv8inc=$(STAGING_DIR_HOSTPKG)/include/node \
	--without-pcre \
	--without-tcl \
	--without-perl5 \
	--without-octave \
	--without-scilab \
	--without-java \
	--without-android \
	--without-guile \
	--without-mzscheme \
	--without-ruby \
	--without-php \
	--without-ocaml \
	--without-csharp \
	--without-lua \
	--without-r \
	--without-go \
	--without-d \
	--disable-ccache


define Package/swig/description
  tool that generates bindings for various languages
endef

define Host/Configure
	(cd $(HOST_BUILD_DIR); ./autogen.sh );
	$(call Host/Configure/Default)
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,swig))
