# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=xorgproto
pkgver=2018.2
pkgrel=1
pkgdesc="combined X.Org X11 Protocol headers"
arch=('any')
url="https://xorg.freedesktop.org/"
license=('custom')
makedepends=('xorg-util-macros' 'meson') # 'xmlto' 'libxslt' 'linuxdoc-tools' 'docbook-sgml' 'fop')
provides=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
conflicts=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
replaces=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
source=(https://xorg.freedesktop.org/archive/individual/proto/$pkgname-$pkgver.tar.bz2{,.sig})
sha512sums=('29ac0479de321eb921b1d902e4670e9e856f8b50c95c07a855aea122e5c9762ff34d01dbda9c795e4c652b09e21151f024aa7ba54bd463e14263db5240418862'
            'SKIP')
validpgpkeys=('995ED5C8A6138EB0961F18474C09DD83CAAA50B2') #  "Adam Jackson <ajax@nwnk.net>"

prepare() {
  mkdir build
}

build() {
  arch-meson $pkgname-$pkgver build

  ninja -C build
}

check() {
  meson test -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install

  # missing docs
  install -m755 -d "${pkgdir}/usr/share/doc/${pkgname}"
  install -m644 $pkgname-$pkgver/*.txt "${pkgdir}/usr/share/doc/${pkgname}/"
  install -m644 $pkgname-$pkgver/PM_spec "${pkgdir}/usr/share/doc/${pkgname}/"
  rm ${pkgdir}/usr/share/doc/${pkgname}/meson_options.txt

  # licenses
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 $pkgname-$pkgver/COPYING* "${pkgdir}/usr/share/licenses/${pkgname}/"

  # cleanup
  rm -f ${pkgdir}/usr/include/X11/extensions/{apple,windows}*
  rm -f ${pkgdir}/usr/share/licenses/${pkgname}/COPYING-{apple,windows}wmproto
  rm -f ${pkgdir}/usr/share/pkgconfig/{apple,windows}wmproto.pc
}
