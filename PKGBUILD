# Maintainer: AndyRTR <andyrtr@archlinux.org>

pkgname=xorgproto
pkgver=2018.1
pkgrel=1
pkgdesc="combined X.Org X11 Protocol headers"
arch=('any')
url="https://xorg.freedesktop.org/"
license=('custom')
makedepends=('xorg-util-macros') # 'xmlto' 'libxslt' 'linuxdoc-tools' 'docbook-sgml' 'fop')
provides=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
conflicts=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
replaces=('bigreqsproto' 'compositeproto' 'damageproto' 'dmxproto' 'dri2proto' 'dri3proto' 'fixesproto' 'fontsproto' 'glproto' 'inputproto' 'kbproto' 'presentproto' 'printproto' 'randrproto' 'recordproto' 'renderproto' 'resourceproto' 'scrnsaverproto' 'videoproto' 'xcmiscproto' 'xextproto' 'xf86dgaproto' 'xf86driproto' 'xf86miscproto' 'xf86vidmodeproto' 'xineramaproto' 'xproto')
source=(https://xorg.freedesktop.org/archive/individual/proto/$pkgname-$pkgver.tar.bz2{,.sig})
sha512sums=('eaad8947f8cda4683bd952706feaa926eed06c508925d3bed7c9a610f925844d3546bbfe49b5403220ca812d63442ca6a72e65ecc50a71899aadf60875156800'
            'SKIP')
validpgpkeys=('995ED5C8A6138EB0961F18474C09DD83CAAA50B2') #  "Adam Jackson <ajax@nwnk.net>"

build() {
  cd "$pkgname-$pkgver"
  # do not try to build additional docs, we don't have xorg-sgml-doctools
  ./configure --prefix=/usr \
    --without-xmlto \
    --without-xsltproc \
    --without-fop
  make
}

check() {
  cd "$pkgname-$pkgver"
  make -k check
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir/" install

  # licenses
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING* "${pkgdir}/usr/share/licenses/${pkgname}/"

  # cleanup
  rm -f ${pkgdir}/usr/include/X11/extensions/{apple,windows}*
  rm -f ${pkgdir}/usr/share/licenses/${pkgname}/COPYING-{apple,windows}wmproto
  rm -f ${pkgdir}/usr/share/pkgconfig/{apple,windows}wmproto.pc
}
