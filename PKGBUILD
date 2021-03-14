#Creater: abcd567
#Maintener: abcd567

pkgname=dump1090-fa
pkgver=latest
pkgrel=1
arch=('x86_64' 'i686' 'armh6' 'armh7' 'armv6l' 'armv7l' 'armv6h' 'armv7h' 'aarch64')
license=('GPL')

makedepends=('git')
depends=('rtl-sdr' 'lighttpd' 'bladerf')
conflicts=('dump1090' 
           'dump1090-mutability' 
           'dump1090-mutability-git'
           'dump1090-fa-git'
           'dump1090-git' 
           'dump1090_mr-git')

source=('dump1090::git+git://github.com/flightaware/dump1090')
md5sums=('SKIP')

install="foo.install"

pkgver() {
  cd $srcdir/dump1090
  printf "%s" "$(git describe --tags | sed 's/-.*//')"
}

build() {
  cd ${srcdir}/dump1090
  make DUMP1090_VERSION=$(git describe --tags | sed 's/-.*//') 
}

package() {
  mkdir -p ${pkgdir}/usr/bin
  cp  ${srcdir}/dump1090/dump1090  ${pkgdir}/usr/bin/dump1090-fa
  cp  ${srcdir}/dump1090/view1090  ${pkgdir}/usr/bin/view1090

  mkdir -p ${pkgdir}/usr/share/dump1090-fa/html
  cp -r ${srcdir}/dump1090/public_html/*  ${pkgdir}/usr/share/dump1090-fa/html/
  
  mkdir -p ${pkgdir}/usr/share/skyaware/html
  cp -r ${srcdir}/dump1090/public_html_merged/*  ${pkgdir}/usr/share/skyaware/html
  
  mkdir -p ${pkgdir}/usr/lib/dump1090-fa/
  cp -r ${srcdir}/dump1090/starch-benchmark  ${pkgdir}/usr/lib/dump1090-fa/
  cp -r ${srcdir}/dump1090/debian/generate-wisdom ${pkgdir}/usr/share/dump1090-fa/
  
  cp -r ${srcdir}/dump1090/debian/start-dump1090-fa ${pkgdir}/usr/share/dump1090-fa/
  
  mkdir -p ${pkgdir}/etc/default
  cp ${srcdir}/dump1090/debian/dump1090-fa.default  ${pkgdir}/etc/default/dump1090-fa
  
  mkdir -p ${pkgdir}/usr/lib/systemd/system
  cp ${srcdir}/dump1090/debian/dump1090-fa.service  ${pkgdir}/usr/lib/systemd/system/dump1090-fa.service

  mkdir -p ${pkgdir}/etc/lighttpd/conf.d
  cp -r ${srcdir}/dump1090/debian/lighttpd/* ${pkgdir}/etc/lighttpd/conf.d
  mkdir -p ${pkgdir}/usr/share/dump1090-fa/bladerf
  cp -r ${srcdir}/dump1090/bladerf/* ${pkgdir}/usr/share/dump1090-fa/bladerf

}
