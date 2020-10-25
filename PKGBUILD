# Maintainer: SkyyySi

pkgname=calamares-git
_pkgname=calamares
pkgver=0.1.r4.g1ca274a
pkgrel=1
pkgdesc='Graphical Arch Linux installer'
arch=('i686' 'x86_64')
license=('GPL')
url='https://github.com/SkyyySi/calamares-arch'
provides=('calamares')
conflicts=('calamares')
depends=('kconfig'
         'kcoreaddons'
         'kiconthemes'
         'ki18n'
         'kio'
         'solid'
         'yaml-cpp'
         'kpmcore>=4.1.0'
         'boost'
         'boost-libs'
         'hwinfo'
         'qt5-svg'
         'polkit-qt5'
         'gtk-update-icon-cache'
         'plasma-framework'
         'qt5-xmlpatterns'
         'squashfs-tools'
         'libpwquality'
         'appstream-qt'
)
source=(
        "$_pkgname::git+$url"
        "20-nopasswd-calamares.rules"
)
sha256sums=(
            "SKIP"
            "c9b7cae731437bad71c1387543d85cf658ed14fd112bec003d1b0e28d7e5a364"
)

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cd ${srcdir}/calamares
	mkdir -p build && cd build
	cmake .. -DCMAKE_INSTALL_PREFIX=/usr
	make -j16
}

package() {
	cd ${srcdir}/calamares/build
	make DESTDIR="$pkgdir" install
	cd ..
	install -Dm644 "settings.conf" "$pkgdir/etc/calamares/settings.conf"
	mkdir -p "$pkgdir/etc/calamares/branding"
	cp -r "src/branding/archlinux" "$pkgdir/etc/calamares/branding/archlinux"
	cp -r "configs" "$pkgdir/etc/calamares/modules"
	install -Dm644 "$srcdir/20-nopasswd-calamares.rules" "$pkgdir/etc/polkit-1/rules.d/20-nopasswd-calamares.rules"
}
