#Creater: abcd567
#Maintener: abcd567

pkgname=dump1090-fa
pkgver=latest
pkgrel=1
arch=('x86_64' 'armh6' 'armh7' 'armv6h' 'armv7h')
license=('GPL')

depends=('rtl-sdr' 'lighttpd' 'bladerf')
conflicts=('dump1090' 
           'dump1090-mutability' 
           'dump1090-mutability-git'
           'dump1090-fa-git'
           'dump1090-git' 
           'dump1090_mr-git')

function checkPkg {
  echo ""
  echo "CHECKING TOOLS NEEDED TO BUILD THE PACKAGE ....."
  echo ""
  if [[ ! `pacman -Qqe $1` ]]
  then
     echo ".... Installing" $1;

  yes | sudo pacman -Sy $1;
  else
     echo $1 "is already installed .......";
  fi
}

checkPkg git
checkPkg make
checkPkg pkgconf
checkPkg binutils
checkPkg gcc
checkPkg fakeroot


source=('dump1090::git+git://github.com/flightaware/dump1090')
md5sums=('SKIP')

install="foo.install"
 
build() {
  cd ${srcdir}/dump1090
  make
}

package() {

  mkdir -p ${pkgdir}/usr/bin
  cp  ${srcdir}/dump1090/dump1090  ${pkgdir}/usr/bin/dump1090-fa

  mkdir -p ${pkgdir}/usr/share/dump1090-fa/html
  cp -r ${srcdir}/dump1090/public_html/*  ${pkgdir}/usr/share/dump1090-fa/html/

  mkdir -p ${pkgdir}/etc/default
  cp ${srcdir}/dump1090/debian/dump1090-fa.default  ${pkgdir}/etc/default/dump1090-fa
  
  mkdir -p ${pkgdir}/usr/lib/systemd/system
  cp ${srcdir}/dump1090/debian/dump1090-fa.service  ${pkgdir}/usr/lib/systemd/system/dump1090-fa.service

  cp -r ${srcdir}/dump1090/debian/lighttpd ${pkgdir}/lighttpd

}
