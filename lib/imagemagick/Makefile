#
# Copyright (C) 2024 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imagemagick
PKG_MAJOR_VERSION:=7
PKG_VERSION:=7.0.8
PKG_REVISION:=46
PKG_RELEASE:=3

PKG_BUILD_DIR:=$(BUILD_DIR)/ImageMagick-$(PKG_VERSION)-$(PKG_REVISION)
PKG_SOURCE:=ImageMagick-$(PKG_VERSION)-$(PKG_REVISION).tar.xz
PKG_SOURCE_URL:=http://mirror.checkdomain.de/imagemagick/releases \
	https://fossies.org/linux/misc/legacy
PKG_HASH:=7cda36ae15890fa81a198bbb8ad577c033fbf5cc0284cb7d12197dfdea25b0fb

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=aclocal.m4 m4/libtool.m4
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

define Package/imagemagick/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=imagemagick
  URL:=http://image_magick.veidrodis.com/
endef

define Package/imagemagick
  $(call Package/imagemagick/Default)
  DEPENDS:=+libpthread +libltdl +libjpeg +libtiff +zlib
endef

define Package/imagemagick/description
  An image manipulation library.
endef

define Package/imagemagick-jpeg
  $(call Package/imagemagick/Default)
  TITLE+= (jpeg)
  DEPENDS:=+imagemagick
endef

define Package/imagemagick-jpeg/description
  imagemagick JPEG module
endef

define Package/imagemagick-png
  $(call Package/imagemagick/Default)
  TITLE+= (png)
  DEPENDS:=+imagemagick +libpng
endef

define Package/imagemagick-png/description
  imagemagick PNG module
endef

define Package/imagemagick-tools
  $(call Package/imagemagick/Default)
  TITLE+= (tools)
  DEPENDS:=+imagemagick
endef

define Package/imagemagick-png/description
  imagemagick tools (mogrify,convert)
endef

define Package/imagemagick-tiff
  $(call Package/imagemagick/Default)
  TITLE+= (tiff)
  DEPENDS:=+imagemagick
endef

define Package/imagemagick-tiff/description
  imagemagick TIFF module
endef


CONFIGURE_ARGS += \
	--with-modules \
	--enable-shared \
	--enable-static \
	--without-pango \
	--without-bzlib \
	--without-freetype \
	--without-fontconfig \
	--without-rsvg \
	--without-fftw \
	--without-xml \
	--without-x \
	--without-magick-plus-plus \
	--without-lzma \
	--without-lcms \
	--without-jbig \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -I$(PKG_BUILD_DIR)/include/linux -I$(PKG_BUILD_DIR)/include"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/* \
		$(1)/usr/include/

	ln -s ImageMagick-$(PKG_MAJOR_VERSION)/MagickCore $(1)/usr/include/magick
	ln -s ImageMagick-$(PKG_MAJOR_VERSION)/MagickWand $(1)/usr/include/wand

	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/

	$(INSTALL_DIR) $(1)/usr/lib/ImageMagick-$(PKG_VERSION)/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/* \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/
endef

define Package/imagemagick/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

define Package/imagemagick-tools/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/{animate,compare,composite,conjure,convert,display,identify,import,magick,magick-script,mogrify,montage,stream} \
		$(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/ImageMagick-7
	$(CP) $(PKG_INSTALL_DIR)/etc/ImageMagick-7/*.xml $(1)/etc/ImageMagick-7/

endef

define BuildPlugin
  define Package/imagemagick-$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q16HDRI/coders
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q16HDRI/coders/$(1).so \
		$$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q16HDRI/coders
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q16HDRI/coders/$(1).la \
		$$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q16HDRI/coders
  endef

  $$(eval $$(call BuildPackage,imagemagick-$(1)))
endef

$(eval $(call BuildPackage,imagemagick))
$(eval $(call BuildPackage,imagemagick-tools))
$(eval $(call BuildPlugin,jpeg))
$(eval $(call BuildPlugin,png))
$(eval $(call BuildPlugin,tiff))
