include $(TOPDIR)/rules.mk

PKG_NAME:=zbar
PKG_VERSION:=0.1.0
PKG_SOURCE_DATE:=2019-05-20
PKG_LICENSE:=LGPL-2.1

PKG_SOURCE_URL:=https://github.com/ZBar/ZBar.git
PKG_SOURCE_PROTO:=git
PKG_RELEASE:=1
PKG_SOURCE_VERSION:=67003d2a985b5f9627bee2d8e3e0b26d0c474b57

PKG_FIXUP:=libtool
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1
PKG_MAINTAINER:=Han Pengfei <pengphei@foxmail.com>

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include

define Package/zbar
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=zbar
  URL:=http://zbar.sourceforge.net/
  DEPENDS:=+libstdcpp +libpthread +librt +imagemagick
endef

define Package/zbar/description
  A comprehensive software suite for reading barcodes. 
  Supports EAN/UPC, Code 128, Code 39, Interleaved 2 of 5 
  and QR Code. Includes libraries and applications for 
  decoding captured barcode images and using a video 
  device (eg, webcam) as a barcode scanner.
endef

CONFIGURE_ARGS+= \
	--disable-docs \
	--with-imagemagick \
	--without-gtk \
	--without-python \
	--without-qt

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.{a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
endef

define Package/zbar/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,zbar))
