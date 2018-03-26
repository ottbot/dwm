pkgname=dwm
pkgver=6.1.26.g3bd8466
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft')
makedepends=('git')
install=dwm.install
provides=('dwm')
conflicts=('dwm')
source=(dwm.desktop
        config.h
        pertag.diff
        fakefullscreen.diff
        "$pkgname::git+http://git.suckless.org/dwm")
md5sums=('939f403a71b6e85261d09fc3412269ee'
         '773694853820017b6e0344b65f5d13e0'
         '31899b188639fef08753e8095f603f58'
         '2e27c57d9ec228e3554556d281707ffc'
         'SKIP')
_patches=('fakefullscreen' 'pertag')

pkgver(){
  cd $pkgname
  git describe --tags |sed 's/-/./g'
}

prepare() {
  cp -f config.h $pkgname/config.h
  cd $pkgname


  for p in ${_patches[@]}
  do
    echo "** Applying ${p}.diff"
    patch -Np1 -i "${SRCDEST}/${p}.diff"
  done

}

build() {
  cd $pkgname
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $pkgname
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D ../dwm.desktop "$pkgdir/usr/share/xsessions/dwm.desktop"
}

# vim:set ts=2 sw=2 et:
