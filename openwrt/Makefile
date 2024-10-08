include $(TOPDIR)/rules.mk

PKG_NAME:=UA2F
PKG_VERSION:=4.0.3
PKG_RELEASE:=1

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILE:=LICENSE

PKG_BUILD_DIR:=$(CURDIR)/..
CMAKE_BINARY_SUBDIR:=build

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ua2f
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=Change User-Agent to Fwords on the fly.
  URL:=https://github.com/Zxilly/UA2F
  DEPENDS:=+iptables-mod-conntrack-extra +iptables-mod-nfqueue \
    +iptables-mod-filter +libnetfilter-conntrack +libnetfilter-queue \
    +libpthread
endef

define Package/ua2f/description
  Change User-agent to Fwords to prevent being checked by Dr.Com.
endef

define Package/ua2f/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ua2f $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/config $(1)/etc/init.d $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/ua2f.config $(1)/etc/config/ua2f
	$(INSTALL_BIN) ./files/ua2f.init $(1)/etc/init.d/ua2f
	$(INSTALL_BIN) ./files/ua2f.uci $(1)/etc/uci-defaults/80-ua2f
endef

define Package/ua2f/postinst
#!/bin/sh

# check if we are on real system
[ -n "$${IPKG_INSTROOT}" ] || {
	(. /etc/uci-defaults/80-ua2f) && rm -f /etc/uci-defaults/80-ua2f
	exit 0
}
endef

$(eval $(call BuildPackage,ua2f))
