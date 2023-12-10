# Maintainer: AndyRTR <andyrtr@archlinux.org>

# When releasing a xorgproto version with updated keysyms, rebuild libx11

pkgname=xorgproto-fs
pkgver=2023.2.r11.g4a043d0
pkgrel=1
pkgdesc="combined X.Org X11 Protocol headers"
arch=('any')
url="https://xorg.freedesktop.org/"
license=('custom')
makedepends=('xorg-util-macros' 'meson')
checkdepends=('python-libevdev')
source=(git+https://github.com/RebuildOfArchangelinux/xorgproto-fs.git#branch=fs)
provides=('xorgproto')
conflicts=('xorgproto')
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  git describe --long --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | sed 's/^xorgproto\.//g'
}

prepare() {
  mkdir build
}

build() {
  arch-meson "$pkgname" build
  ninja -C build
}

check() {
  meson test -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install

  # missing docs
  install -m755 -d "${pkgdir}/usr/share/doc/${pkgname}"
  install -m644 "$pkgname"/PM_spec "${pkgdir}/usr/share/doc/${pkgname}/"

  # licenses
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 "$pkgname"/COPYING* "${pkgdir}/usr/share/licenses/${pkgname}/"
  # remove licences of legacy stuff we don't ship anymore
  rm -f "${pkgdir}"/usr/share/licenses/${pkgname}/COPYING-{evieproto,fontcacheproto,lg3dproto,printproto,xcalibrateproto,xf86rushproto}

  # cleanup
  rm -f "${pkgdir}"/usr/include/X11/extensions/apple*
  rm -f "${pkgdir}"/usr/share/licenses/${pkgname}/COPYING-{apple,windows}wmproto
  rm -f "${pkgdir}"/usr/share/pkgconfig/applewmproto.pc
}
