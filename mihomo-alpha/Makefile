include $(TOPDIR)/rules.mk

PKG_NAME:=mihomo-alpha
PKG_VERSION:=2026.09.14~ab405ba

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/MetaCubeX/mihomo.git
PKG_SOURCE_VERSION:=ab405bad5beeeac8b003bb01f60f134f6df54471
PKG_MIRROR_HASH:=add08838200dcacaafc4ddd7e74eb43e16f3c630b4410e2324128c9b3a5f39d3

PKG_LICENSE:=GPL3.0+
PKG_MAINTAINER:=Joseph Mory <morytyann@gmail.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16

PKG_BUILD_VERSION:=alpha-ab405ba

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_TIME:=$(shell date -u -Iseconds)

GO_PKG:=github.com/metacubex/mihomo
GO_PKG_BUILD_PKG:=github.com/metacubex/mihomo
GO_PKG_LDFLAGS_X:=$(GO_PKG)/constant.Version=$(PKG_BUILD_VERSION) $(GO_PKG)/constant.BuildTime=$(PKG_BUILD_TIME)
GO_PKG_TAGS:=with_gvisor
GO_PKG_INSTALL_BIN_PATH:=/usr/libexec

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/mihomo-alpha
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A rule based proxy in Go.
  URL:=https://wiki.metacubex.one
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle +ip-full +kmod-inet-diag +kmod-tun
  PROVIDES:=mihomo
  VARIANT:=alpha
  ALTERNATIVES:=\
    300:/usr/bin/mihomo:/usr/libexec/mihomo-alpha
endef

define Package/mihomo-alpha/description
  A rule based proxy in Go.
endef

define Build/Prepare
	$(Build/Prepare/Default)
	$(RM) -r $(PKG_BUILD_DIR)/rules/logic_test
endef

define Package/mihomo-alpha/install
	$(INSTALL_DIR) $(1)/usr/libexec
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/mihomo $(1)/usr/libexec/mihomo-alpha
endef

$(eval $(call GoBinPackage,mihomo-alpha))
$(eval $(call BuildPackage,mihomo-alpha))
