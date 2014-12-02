# Contributor: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>
# Contributor: Giovanni Scafora <giovanni@archlinux.org>
# Contributor: Jeff Mickey <j@codemac.net>

pkgname=amsn
pkgver=0.98.9
pkgrel=3
pkgdesc="MSN client written in Tcl/Tk"
arch=('i686' 'x86_64')
url="http://amsn.sourceforge.net/"
license=('GPL2')
depends=('tk' 'tls')
makedepends=('libjpeg' 'libpng' 'farstream' 'libv4l')
# not compatible with farstream 0.2
#optdepends=('farstream: for video conferencing')
changelog=$pkgname.changelog
source=(http://downloads.sourceforge.net/sourceforge/$pkgname/$pkgname-$pkgver-src.tar.bz2
        $pkgname-$pkgver-v4l2.patch
        $pkgname-$pkgver-no-rebuild-on-install.patch)
sha256sums=('1fd2620489cc3627a841773a79cf28a7c9c438979c76d37f231a773a79e7f23e'
            '5371339024548fad3b3c5330e3bc410360a383a75d1771fb656885acddfc44cf'
            'dd560bebcfa672ba0be56b70dbcaa069b0faba7206d9cb8ea5d61fbd50ad81a1')

build() {
  cd ${srcdir}/$pkgname-$pkgver

  # patch for linux kernel header changes
  patch -Np0 -i ${srcdir}/$pkgname-$pkgver-v4l2.patch
  # build patch
  patch -Np0 -i ${srcdir}/$pkgname-$pkgver-no-rebuild-on-install.patch

  # python2 fix
  for file in lang/missing.py plugins/music/infosongbird; do
      sed -i 's_/usr/bin/env python_/usr/bin/env python2_' ${file}
  done

  ./configure --prefix=/usr
  make
}

package() {
  cd ${srcdir}/$pkgname-$pkgver

  make DESTDIR=${pkgdir} install
}
