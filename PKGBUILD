#Creater: abcd567
#Maintener: abcd567

pkgname=dump1090-fa
pkgver=latest
pkgrel=1
arch=('x86_64' 'i686' 'armh6' 'armh7' 'armv6l' 'armv7l' 'armv6h' 'armv7h')
license=('GPL')

makedepends=('git')
depends=('rtl-sdr' 'lighttpd' 'bladerf')
conflicts=('dump1090' 
           'dump1090-mutability' 
           'dump1090-mutability-git'
           'dump1090-fa-git'
           'dump1090-git' 
           'dump1090_mr-git')

  echo ""
  echo ""
  echo -e "\e[92m TOOLS REQUIRED TO BUILD PACKAGE ARE:\e[97m"
  echo -e "\e[93m binutils, make, fakeroot, pkgconf, and gcc\e[97m"
  echo -e "\e[97m CHECKING TOOLS, MISSING TOOLS WILL BE OFFERED FOR INSTALLATION ....."
  echo -e "\e[91m \"makepkg\" WILL FAIL IF  MISSING TOOLS ARE NOT INSTALLED \e[97m"
  echo ""
  sudo pacman -Sy --needed binutils make fakeroot pkgconf gcc 

echo -e "\e[93m Cloning source code and starting to build \e[97m"
echo -e "\e[93m It will take a while, please wait.... \e[97m"

source=('dump1090::git+git://github.com/flightaware/dump1090')
md5sums=('SKIP')

install="foo.install"

pkgver() {
  cd $srcdir/dump1090
  printf "%s" "$(git describe --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g')"
}

build() {
  cd ${srcdir}/dump1090
  make all faup1090 EXTRACFLAGS=-DHTMLPATH=\\\"/usr/share/dump1090/html\\\"
}

package() {

  mkdir -p ${pkgdir}/usr/bin
  cp  ${srcdir}/dump1090/dump1090  ${pkgdir}/usr/bin/dump1090-fa
  cp  ${srcdir}/dump1090/view1090  ${pkgdir}/usr/bin/view1090

  mkdir -p ${pkgdir}/usr/lib/piaware/helpers
  cp -r ${srcdir}/dump1090/faup1090  ${pkgdir}/usr/lib/piaware/helpers/faup1090

  mkdir -p ${pkgdir}/usr/share/dump1090-fa/html
  cp -r ${srcdir}/dump1090/public_html/*  ${pkgdir}/usr/share/dump1090-fa/html/
  cp -r ${srcdir}/dump1090/debian/start-dump1090-fa ${pkgdir}/usr/share/dump1090-fa/
  
  mkdir -p ${pkgdir}/etc/default
  cp ${srcdir}/dump1090/debian/dump1090-fa.default  ${pkgdir}/etc/default/dump1090-fa
  
  mkdir -p ${pkgdir}/usr/lib/systemd/system
  cp ${srcdir}/dump1090/debian/dump1090-fa.service  ${pkgdir}/usr/lib/systemd/system/dump1090-fa.service

  cp -r ${srcdir}/dump1090/debian/lighttpd ${pkgdir}/lighttpd

}
