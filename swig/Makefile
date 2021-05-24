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
PKG_SOURCE_VERSION:=e82725b22e9352f269875ecee0c868dd434a04fb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=81bf3e1fdf72a86aa753c1d4ce42b3d852cb9679208e64fd2ca6495aae0fcba9

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>, Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

HOST_BUILD_DEPENDS:=python3/host node/host
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
