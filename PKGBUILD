# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/libinput
# 						Maintainer: Andreas Radke <andyrtr@archlinux.org>
# 						Maintainer: Jan de Groot

pkgname=libinput
pkgver=1.9.1
pkgrel=2
pkgdesc="Input device management and event handling library"
arch=(x86_64)
url="https://www.freedesktop.org/software/libinput/"
license=(custom:X11)
depends=('mtdev' 'libevdev' 'libwacom')
makedepends=('doxygen' 'graphviz' 'gtk3' 'meson')
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure')
provides=("libinput=${pkgver}")
source=(https://freedesktop.org/software/${pkgname}/${pkgname}-$pkgver.tar.xz)
sha512sums=('e60c401cdec6b862c6c7186e636bba285e229b82998d9f86940659806bb64c295ec1060b5e8065345668e4b3ff95457bd01327351520d9f6cf8cbc98b9b95da0')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
  cd $pkgname-$pkgver
  # Reduce docs size
  printf '%s\n' >>doc/libinput.doxygen.in \
  HAVE_DOT=yes DOT_IMAGE_FORMAT=svg INTERACTIVE_SVG=yes
}

build() {
  arch-meson $pkgname-$pkgver build -Dtests=false
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install

  install -Dvm644 $pkgname-$pkgver/COPYING \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # install doc - no Makefile target
  install -d "$pkgdir/usr/share/doc"
  cp -av build/html "$pkgdir/usr/share/doc/libinput"
}
