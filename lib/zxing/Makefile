include $(TOPDIR)/rules.mk

PKG_NAME:=zxing
PKG_VERSION:=1.0.0
PKG_SOURCE_DATE:=2019-05-23
PKG_LICENSE:=Apache-2.0

PKG_SOURCE_URL:=https://github.com/glassechidna/zxing-cpp.git
PKG_SOURCE_PROTO:=git
PKG_RELEASE:=1
PKG_SOURCE_VERSION:=e0e40ddec63f38405aca5c8c1ff60b85ec8b1f10

PKG_FIXUP:=libtool
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/
PKG_BUILD_PARALLEL:=1
PKG_MAINTAINER:=Han Pengfei <pengphei@foxmail.com>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include

define Package/zxing
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=zxing
  URL:=https://zxing.org
  DEPENDS:=+libstdcpp +libpthread
endef

define Package/zxing/description
  ZXing (pronounced "zebra crossing") is an open-source, 
  multi-format 1D/2D barcode image processing library 
  implemented in Java, with ports to other languages.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.{a,so*} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
endef

define Package/zxing/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,zxing))
