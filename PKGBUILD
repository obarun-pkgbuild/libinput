# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libinput
# 						Maintainer: Andreas Radke <andyrtr@archlinux.org>
# 						Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.8.2
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
sha512sums=('555a7680cc8aaf62c5370a865f3aff0a933d42d94a3d8861c072666b02c9e1be45ea39de9a749a9575cdfb613b6150e412e18559d94d4919f21ca4680a3c76a7')
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
