# Maintainer: udeved <udeved@openrc4arch.site40.net>

# file vars for easy update
_Ifrcon=fcron.init.3
_Crsysl=rsyslog.confd
_Irsysl=rsyslog.initd
_Csane=saned.confd
_Isane=saned.initd
_Ifuse=fuse.init
_Cmeta=metalog.confd
_Imeta=metalog.initd
_Csyslog=syslog-ng.confd
_Isyslog=syslog-ng.rc6
_Clirc1=lircd.conf.4
_Clirc2=irexec-confd
_Ilirc1=lircd-0.8.6-r2
_Ilirc2=irexec-initd-0.8.6-r2
_Ilirc3=lircmd
#_Csens=sensord-conf.d
_Isens1=sensord-4-init.d
_Isens2=fancontrol-init.d-2
_Isens3=lm_sensors-3-init.d
_Ccpu=conf.d-r2
_Icpu=init.d-r4
_Cntp1=ntpd.confd
_Cntp2=ntp-client.confd
_Cntp3=sntp.confd
_Intp1=ntpd.rc
_Intp2=ntp-client.rc
_Intp3=sntp.rc

_gentoo_uri="http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86"

pkgbase=openrc-misc-split
pkgname=openrc-misc-split
true && pkgname=('cpupower-openrc'
				'fcron-openrc'
				'fuse-openrc'
				'metalog-openrc'
				'rsyslog-openrc'
				'sane-openrc'
				'syslog-ng-openrc'
				'lirc-utils-openrc'
				'lm_sensors-openrc'
				'ntp-openrc'
				'openrc-misc-split')
pkgver=20140415
pkgrel=1
pkgdesc="OpenRC init scripts"
arch=('any')
url="https://github.com/udeved/pkgbuilds"
license=('GPL2')
groups=('openrc' 'openrc-misc')
makedepends=('cpupower'
			'fcron'
			'fuse'
			'metalog'
			'ntp' 'rsyslog'
			'sane' 'syslog-ng'
			'lirc-utils'
			'lm_sensors')
conflicts=('openrc-arch-services-git'
			'initscripts'
			'systemd-sysvcompat'
			'openrc'
			'openrc-git')

source=("${_gentoo_uri}/sys-process/fcron/files/${_Ifrcon}"
		"${_gentoo_uri}/app-admin/rsyslog/files/7-stable/${_Crsysl}"
		"${_gentoo_uri}/app-admin/rsyslog/files/7-stable/${_Irsysl}"
		"${_gentoo_uri}/media-gfx/sane-backends/files/${_Csane}"
		"${_gentoo_uri}/media-gfx/sane-backends/files/${_Isane}"
		"${_gentoo_uri}/sys-fs/fuse/files/${_Ifuse}"
		"${_gentoo_uri}/app-admin/metalog/files/${_Cmeta}"
		"${_gentoo_uri}/app-admin/metalog/files/${_Imeta}"
		"${_gentoo_uri}/app-admin/syslog-ng/files/3.5/${_Csyslog}"
		"${_gentoo_uri}/app-admin/syslog-ng/files/3.5/${_Isyslog}"
		"${_gentoo_uri}/app-misc/lirc/files/${_Clirc1}"
		"${_gentoo_uri}/app-misc/lirc/files/${_Clirc2}"
		"${_gentoo_uri}/app-misc/lirc/files/${_Ilirc1}"
		"${_gentoo_uri}/app-misc/lirc/files/${_Ilirc2}"
		"${_gentoo_uri}/app-misc/lirc/files/${_Ilirc3}"
		"${_gentoo_uri}/sys-power/cpupower/files/${_Ccpu}"
		"${_gentoo_uri}/sys-power/cpupower/files/${_Icpu}"
		#"${_gentoo_uri}/sys-apps/lm_sensors/files/${_Csens}"
		"${_gentoo_uri}/sys-apps/lm_sensors/files/${_Isens1}"
		"${_gentoo_uri}/sys-apps/lm_sensors/files/${_Isens2}"
		"${_gentoo_uri}/sys-apps/lm_sensors/files/${_Isens3}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Cntp1}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Cntp2}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Cntp3}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Intp1}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Intp2}"
		"${_gentoo_uri}/net-misc/ntp/files/${_Intp3}")

pkgver() {
	date +%Y%m%d
}

_shebang='s|#!/sbin/runscript|#!/usr/bin/runscript|'
_runpath='s|/var/run|/run|g'
_binpath='s|/usr/sbin|/usr/bin|g'


package_cpupower-openrc() {
	true
	pkgdesc="OpenRC cpupower init script"
	depends=('openrc-base' 'cpupower')
	backup=('etc/conf.d/cpupower')
	install=cpupower.install

	install -Dm755 "${srcdir}/${_Ccpu}" "${pkgdir}/etc/conf.d/cpupower"
	install -Dm755 "${srcdir}/${_Icpu}" "${pkgdir}/etc/init.d/cpupower"

	sed -e "${_shebang}" -i "${pkgdir}/etc/init.d/cpupower"
}

package_fcron-openrc() {
	true
	pkgdesc="OpenRC fcron init script"
	depends=('openrc-base' 'fcron')
	groups=('openrc-misc')
	provides=('openrc-cron')
	conflicts=('cronie' 'cronie-openrc' 'openrc-arch-services-git'
		  'initscripts' 'systemd-sysvcompat' 'openrc' 'openrc-git')
	install=fcron.install

	install -Dm755 "${srcdir}/${_Ifrcon}" "${pkgdir}/etc/init.d/fcron"

	local _p1='s|/usr/libexec|/usr/bin|g'
	sed -e "${_shebang}" -e "${_runpath}" -e "${_p1}" -i "${pkgdir}/etc/init.d/fcron"
}

package_ntp-openrc() {
	true
	pkgdesc="OpenRC ntp init script"
	depends=('openrc-base' 'ntp')
	optdepends=('bind-openrc')
	provides=('openrc-timed')
	conflicts=('openntpd-openrc' 'openntpd' 'openrc-arch-services-git'
		  'initscripts' 'systemd-sysvcompat' 'openrc' 'openrc-git')
	backup=('etc/conf.d/ntpd' 'etc/conf.d/ntp-client' 'etc/init.d/sntp')
	install=ntp.install

	install -Dm755 "${srcdir}/${_Cntp1}" "${pkgdir}/etc/conf.d/ntpd"
	install -Dm755 "${srcdir}/${_Intp1}" "${pkgdir}/etc/init.d/ntpd"
	install -Dm755 "${srcdir}/${_Cntp2}" "${pkgdir}/etc/conf.d/ntp-client"
	install -Dm755 "${srcdir}/${_Intp2}" "${pkgdir}/etc/init.d/ntp-client"
	install -Dm755 "${srcdir}/${_Cntp3}" "${pkgdir}/etc/conf.d/sntp"
	install -Dm755 "${srcdir}/${_Intp3}" "${pkgdir}/etc/init.d/sntp"

	for f in ${pkgdir}/etc/init.d/*;do
	  sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i $f
	done
}

package_rsyslog-openrc() {
	true
	pkgdesc="OpenRC rsyslog init script"
	depends=('openrc-base' 'rsyslog')
	backup=('etc/conf.d/rsyslog')
	install=rsyslog.install

	install -Dm755 "${srcdir}/${_Crsysl}" "${pkgdir}/etc/conf.d/rsyslog"
	install -Dm755 "${srcdir}/${_Irsysl}" "${pkgdir}/etc/init.d/rsyslog"

	sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i "${pkgdir}/etc/init.d/rsyslog"
}

package_sane-openrc() {
	true
	pkgdesc="OpenRC sane init script"
	depends=('openrc-base' 'sane')
	backup=('etc/conf.d/saned')
	install=sane.install

	install -Dm755 "${srcdir}/${_Csane}" "${pkgdir}/etc/conf.d/saned"
	install -Dm755 "${srcdir}/${_Isane}" "${pkgdir}/etc/init.d/saned"

	sed -e "${_shebang}" -e "${_runpath}" -e "${_binpath}" -i ${pkgdir}/etc/init.d/saned
}

package_fuse-openrc(){
	true
	pkgdesc="OpenRC fuse init script"
	depends=('openrc-base' 'fuse')
	install=fuse.install

	install -Dm755 "${srcdir}/${_Ifuse}" "${pkgdir}/etc/init.d/fuse"
	sed -e "${_shebang}" -i "${pkgdir}/etc/init.d/fuse"
}

package_metalog-openrc() {
	true
	pkgdesc="OpenRC metalog init script"
	depends=('openrc-base' 'metalog')
	backup=('etc/conf.d/metalog')
	install=metalog.install

	install -Dm755 "${srcdir}/${_Cmeta}" "${pkgdir}/etc/conf.d/metalog"
	install -Dm755 "${srcdir}/${_Imeta}" "${pkgdir}/etc/init.d/metalog"

	sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i "${pkgdir}/etc/init.d/metalog"
}

package_syslog-ng-openrc() {
	true
	pkgdesc="OpenRC syslog-ng init script"
	depends=('openrc-base' 'syslog-ng')
	backup=('etc/conf.d/syslog-ng')
	install=syslog-ng.install

	install -Dm755 "${srcdir}/${_Csyslog}" "${pkgdir}/etc/conf.d/syslog-ng"
	install -Dm755 "${srcdir}/${_Isyslog}" "${pkgdir}/etc/init.d/syslog-ng"

	sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i "${pkgdir}/etc/init.d/syslog-ng"
}

package_lm_sensors-openrc() {
	true
	pkgdesc="OpenRC lm_sensors init script"
	depends=('openrc-base' 'lm_sensors')
	#backup=('etc/conf.d/sensord')
	install=lm_sensors.install

	#install -Dm755 "${srcdir}/${_Csens}" "${pkgdir}/etc/conf.d/sensord"
	install -Dm755 "${srcdir}/${_Isens1}" "${pkgdir}/etc/init.d/sensord"
	install -Dm755 "${srcdir}/${_Isens2}" "${pkgdir}/etc/init.d/fancontrol"
	install -Dm755 "${srcdir}/${_Isens3}" "${pkgdir}/etc/init.d/lm_sensors"

	for f in ${pkgdir}/etc/init.d/*;
	do
	  sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i $f
	done
}

package_lirc-utils-openrc() {
	true
	pkgdesc="OpenRC lirc-utils init script"
	depends=('openrc-base' 'lirc-utils')
	backup=('etc/conf.d/lircd' 'etc/conf.d/irexec')
	install=lirc-utils.install

	install -Dm755 "${srcdir}/${_Clirc1}" "${pkgdir}/etc/conf.d/lircd"
	install -Dm755 "${srcdir}/${_Ilirc1}" "${pkgdir}/etc/init.d/lircd"

	install -Dm755 "${srcdir}/${_Clirc2}" "${pkgdir}/etc/conf.d/irexec"
	install -Dm755 "${srcdir}/${_Ilirc2}" "${pkgdir}/etc/init.d/irexec"

	install -Dm755 "${srcdir}/${_Ilirc3}" "${pkgdir}/etc/init.d/lircmd"

	for f in ${pkgdir}/etc/init.d/*;do
	  sed -e "${_shebang}" -e "${_binpath}" -e "${_runpath}" -i $f
	done
}

# Comment out if you build for your personal repo
# remove 'openrc-misc-split' from pkgname array
# Dummy package to make AUR display correct info
# If installed, it should make upgrade from AUR possible
package_openrc-misc-split() {
	true
	pkgdesc="OpenRC misc init scripts, AUR upgrade and info split-pkg helper"
	depends=('openrc-base')
	provides=("openrc-misc-split-helper=${pkgver}")
}

sha256sums=('ceada7a1c9e8b62cff506bc94a1813706c7de1ed23daf9c3450ad549df4fafb7'
            'ff2634927d3208ac2c82d352f0a7dc9fef1d0ee098d18f818d4417ac04516e9c'
            '7b3b32e89c051566b68c5e5a077cd5960da183e071e411b1248d4e4702a24279'
            '197e44ba1f438a18f5f7d9f5858feb19c1ece4286d82a5e63caf9be5b964aa76'
            '4dd4e7fa07bf2ab2d4f5753156f5df0ad2277523f6755b0eab3d2db3480989e2'
            '22a22c914d2a4f0fb5fc8495f4b7efcd1819efde548c9033ca612c181cd29eda'
            'ec9f05b386a06a4b2d5398cc0c33f34eba3f5e74ad46ae203d682f8ebc593f99'
            '906c31e0817517dc6c141a7a10565140ea272d3c958a065f520a0ecb6f81912f'
            'd28c269c8aa2876a389aefdc76b18bcd30eb6653ea1e54a0eb6fb596568643b6'
            '9e5ba6d869b99d835cde702a028dae89935c234a14dad79e00a3b5e6379e1f91'
            'd36ff77fa193a065d25e373723e03f1a9471205151b82c73a6574cce4f095962'
            'c404ad3b624004cab25bd3a89593cdeb0abbc25771d6e52caf2f37cb4f7b2b79'
            '1b1f2970cc81a6053fcb6c0ead786436b6423c67170087dde283e54f32ae16e5'
            '5e5a31fbd93294a6e210499a880fcab371b23706824c9d60d827b0187d7bade4'
            'd47f22a33a83c14a4a0c333d6a445c40e550c491899fb0c6d323e23fe1eac7b7'
            '9ab6f022d2b2948660decf5e383984e6ddb9e9e5e6e2761c3031378ddd87e947'
            '25f2a1665c88dc5227698bdedc2098d6e37d12d8b966f00e2a180c95a33cc8b4'
            '4bd482a54decc5a51aee60e19ae31b0182d5857b112754247f04c0829b159b07'
            '36d489296c31736f8015b0ce27052b3f1555b7fe6335120c0477b044b8e4fb8d'
            '9b018f9f7a0975988387858823fe59a5cd8af6413d8c3170db0e24aac6021ec3'
            '40803821f498267f6567436eedc18201b5ae4b5390d6872fb15a94200c2ac06f'
            'c7dc517cdb5ee10e2a07ccea15ec47ba0b7aff8ac1469204c8d7faf71bcae2c5'
            '97282007801cb9c0e3b431e2930dec3bb8ce8869f63f7e02d903846e96734684'
            'f7c58e8f8e91ee0c1b947e9684b0a9e9e27220e0c97a8b06ee4e3bc5578a88b2'
            '2e4a42dd64b7c6dacfcfefdab8dc1e7c45d7a0966ef8b928583d18393362c719'
            '8fbd405ad951e7ad046e4408abb98f4066077113187198767d52f28d7228bae4')
