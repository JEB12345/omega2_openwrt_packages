
include $(TOPDIR)/rules.mk

PKG_NAME:=numpy
PKG_VERSION:=1.16
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=HEAD
PKG_SOURCE_URL:=https://github.com/numpy/numpy.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/numpy
  SECTION:=onion
  CATEGORY:=Onion
  SUBMENU:=Libraries
  TITLE:=numpy
  URL:=https://github.com/numpy/numpy
  DEPENDS:=+python 
endef

define Package/numpy/description
  Numpy, which you know
endef

PYTHON_VERSION = "2.7"
TARGET_CFLAGS += $(FPIC)
TARGET_LIBS += -l m
TARGET_PYINC += "-I$(STAGING_DIR)/usr/include/python$(PYTHON_VERSION)/"

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	CC="$(TARGET_CC)" \
	CFLAGS="$(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	LIB="$(TARGET_LIBS)" \
	PYINC="$(TARGET_PYINC)"
endef

define Package/python-spidev/install
	# install the python module
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON_VERSION)
	$(CP)   $(PKG_BUILD_DIR)/lib/numpy.so $(1)/usr/lib/python$(PYTHON_VERSION)
endef

$(eval $(call BuildPackage,numpy))

