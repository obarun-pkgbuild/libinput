# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libinput
# 						Maintainer: Andreas Radke <andyrtr@archlinux.org>
# 						Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.8.3
pkgrel=2
pkgdesc="Input device management and event handling library"
arch=(x86_64)
url="https://www.freedesktop.org/software/libinput/"
license=(custom:X11)
depends=('mtdev' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
optdepends=('gtk3: libinput debug-gui')
provides=("libinput=${pkgver}")
source=(https://freedesktop.org/software/${pkgname}/${pkgname}-$pkgver.tar.xz)
sha512sums=('88006d217e3507858fa6b9ac1f25c267255fb51d1bcf1208d2afd423bf2a9292944bc5526ea91f27fad3ff04c2f9f43ab3aa25fd9fb7ace1231ecd33ddf18de6')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  mkdir build
  cd $pkgname-$pkgver
}

build() {
  cd build
  meson --prefix=/usr	--buildtype=release ../$pkgname-$pkgver \
						--libexecdir=/usr/lib \
						-Dtests=false
  ninja
}

package() {
  cd build
  DESTDIR="$pkgdir" ninja install

  cd ../$pkgname-$pkgver
  install -Dvm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # install doc - no Makefile target
  install -dv "$pkgdir/usr/share/doc/libinput"
  cp -av doc/html/* "$pkgdir/usr/share/doc/libinput"
}
