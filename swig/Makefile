#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=swig
PKG_VERSION:=4.2.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_HASH:=261ca2d7589e260762817b912c075831572b72ff2717942f75b3e51244829c97

#PKG_SOURCE_PROTO:=git
#PKG_SOURCE_URL:=https://github.com/swig/swig.git
#PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
#PKG_SOURCE_VERSION:=d22b7dfaea1f7abd4f3d0baecc1a1eddff827561
#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
#PKG_MIRROR_HASH:=6eef69f05eadbe6848ad8425a5cfed3736f0533e7dc8ca25ddf84bb018dc956f

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
