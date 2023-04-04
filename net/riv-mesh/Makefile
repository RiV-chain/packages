include $(TOPDIR)/rules.mk

PKG_NAME:=riv-mesh
PKG_VERSION:=0.4.7.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/RiV-Chain/RiV-mesh/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=d211ea511d0cc1e06d394faca40fd3daa184e321a05ac87e6a84a26b5bb0dbf8
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-go-$(PKG_VERSION)

PKG_MAINTAINER:=Vadym Vikulin <vadym.vikulin@rivchain.org>
PKG_LICENSE:=LGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/RiV-Chain/RiV-mesh
GO_PKG_BUILD_PKG:=github.com/RiV-chain/RiV-mesh/cmd/...

GO_PKG_LDFLAGS_X:= \
  github.com/RiV-chain/RiV-mesh/src/version.buildName=mesh-openwrt \
  github.com/RiV-chain/RiV-mesh/src/version.buildVersion=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/riv-mesh
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Routing and Redirection
	TITLE:=RiV-mesh supports end-to-end encrypted IPv6 networks
	URL:=https://github.com/RiV-Chain/
	DEPENDS:=$(GO_ARCH_DEPENDS) @IPV6 +kmod-tun +dkjson +libuci-lua
endef

define Package/riv-mesh/description
 RiV-mesh is an implementation of a fully end-to-end encrypted IPv6 network,
 created in the scope to produce the Transport Layer for RiV Chain Blockchain,
 also to facilitate secure conectivity between a wide spectrum of endpoint
 devices like IoT devices, desktop computers or even routers. It is lightweight,
 self-arranging, supported on multiple platforms and allows pretty much any
 IPv6-capable application to communicate securely with other RiV-mesh nodes.
 RiV-mesh does not require you to have IPv6 Internet connectivity - it also works over IPv4.
endef

define Package/riv-mesh/conffiles
/etc/config/riv-mesh
endef

define Package/riv-mesh/install
	$(INSTALL_DIR) \
		$(1)/etc/init.d \
		$(1)/etc/uci-defaults \
		$(1)/usr/sbin

	$(INSTALL_BIN) \
		$(GO_PKG_BUILD_BIN_DIR)/mesh \
		$(1)/usr/sbin

	$(INSTALL_BIN) \
		$(GO_PKG_BUILD_BIN_DIR)/meshctl \
		$(1)/usr/sbin

	$(INSTALL_BIN) \
		./files/rivuci \
		$(1)/usr/sbin

	$(INSTALL_BIN) \
		./files/riv-mesh.defaults \
		$(1)/etc/uci-defaults/riv-mesh

	$(INSTALL_BIN) \
		./files/riv-mesh.init \
		$(1)/etc/init.d/riv-mesh
endef

$(eval $(call GoBinPackage,riv-mesh))
$(eval $(call BuildPackage,riv-mesh))
