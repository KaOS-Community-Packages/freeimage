pkgname=freeimage
pkgver=3.17.0
pkgrel=1
pkgdesc="Library project for developers who would like to support popular graphics image formats"
arch=('x86_64')
license=('GPL' 'custom:FIPL')
url="http://freeimage.sourceforge.net/"
depends=('gcc-libs')
makedepends=('dos2unix' 'clang') # Remove clang when this compiles with gcc 5.1
source=("http://downloads.sourceforge.net/project/freeimage/Source%20Distribution/${pkgver}/FreeImage${pkgver//./}.zip")
md5sums=('459e15f0ec75d6efa3c7bd63277ead86')

build() {
  cp -r FreeImage FreeImagefip

  export CFLAGS+=" -O3 -fPIC -fexceptions -fvisibility=hidden -DNO_LCMS"
  export CXXFLAGS+=" -O3 -fPIC -fexceptions -fvisibility=hidden -Wno-ctor-dtor-privacy"

  export CC="clang"
  export CXX="clang++"

  cd FreeImage
  make

  cd ${srcdir}/FreeImagefip
  CXX=clang++ make -f Makefile.fip 
}

package() {
  cd FreeImage
  make DESTDIR=${pkgdir} install

  cd ${srcdir}/FreeImagefip
  make -f Makefile.fip DESTDIR=${pkgdir} install

  install -D -m644 ${srcdir}/FreeImage/license-fi.txt ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
}
