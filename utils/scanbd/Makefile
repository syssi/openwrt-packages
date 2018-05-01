#
# Copyright (C) 2015-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=scanbd
PKG_VERSION:=1.5.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=@SF/scanbd
PKG_HASH:=b69ca5a474b81516d19c38082d949363c243df9ab9742315aaae499723267e5f
PKG_BUILD_DIR:=$(PKG_VERSION)

PKG_MAINTAINER:=Sebastian Muszynski <basti@linkt.de>
PKG_LICENSE:=GPL-2.0+

#PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/scanbd
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Scanner button daemon
  URL:=https://sourceforge.net/projects/scanbd/
  DEPENDS:=+libusb-1.0 +confuse +libsane +xinetd +libdbus
endef

define Package/scanbd/description
 It polls the scanner buttons looking for buttons pressed or function knob
 changes or other scanner events as paper inserts / removals and at the same
 time allows also scan-applications to access the scanners. If buttons are
 pressed, etc., various actions can be submitted (scan, copy, email, ...) via
 action scripts. The function knob values are passed to the action-scripts as
 well.
 .
 Scan actions are also signaled via D-Bus. This can be useful for foreign
 applications. Scans can also be triggered via D-Bus from foreign applications.
 .
 On platforms which support signaling of dynamic device insertion / removal
 (libudev, D-Bus, hal) scanbd supports this as well. scanbd can use all
 sane-backends or some special backends from the (old) scanbuttond project.
 .
 This package is a successor of scanbuttond.
endef

define Package/scanbd/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/scanbd/scanbd $(1)/usr/sbin/
	ln -s scanbd $(1)/usr/sbin/scanbm

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/scanbd.init $(1)/etc/init.d/scanbd

	$(INSTALL_DIR) $(1)/etc/scanbd/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/conf/scanbd.conf $(1)/etc/scanbd/
	$(INSTALL_DIR) $(1)/etc/scanbd/scanner.d/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/conf/scanner.d/* $(1)/etc/scanbd/scanner.d/
endef

$(eval $(call BuildPackage,scanbd))
