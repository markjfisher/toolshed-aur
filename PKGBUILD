# Maintainer: Paul Hentschel <aur at hpminc dot com>

pkgname=toolshed
pkgver=2.2
pkgrel=1
pkgdesc="Utilities for Tandy Color Computer and Dragon microcomputers cross-development."
arch=('x86_64')
url="http://toolshed.sourceforge.net"
license=('PerlArtistic')
depends=('fuse2')
makedepends=('discount')
source=("https://downloads.sourceforge.net/$pkgname/$pkgname-$pkgver.tar.gz"
        "ar2-ar-fix.patch"
        "ar2-arsup-fix.patch"
        "ar2-lz1-fix.patch"
        "ar2-o2u-c-fix.patch"
        "ar2-o2u-h-fix.patch"
        "mamou-mamou-fix.patch"
        )
sha256sums=('ab7201970e9c13e1cbdb9c8398bd888f870e75e33055b7a308bb039f67614c69'
            'd85c196d44c0aba13a6bddd5e54e8510291321e9d20d814bb0c5c4d3ea21a0a1'
            'f0ac7fdf8404494ea8ffa484c878be879293bb8ee4debe9bc0d7ef18ab439525'
            '5cbdef4efc02499d2d594d06a5f3963646e6ab0d7e4bc6418eefa3b86fd9bb2f'
            'e0c7b2342d4ed9faf35b996ab2dc7afd6b981af6db90deb4055226391a6f2bf3'
            '11f891a25c3418ed4d3ee6b29bb7fbf7fcd672b0e563a8d817b26c2bc204ffbf'
            '7356ae26452eaeeefecb4fcfd820d116b055922ebbc81590db0d577a1638a923'
            )

prepare() {
  cd "$pkgname-$pkgver"
  
  # Apply patches to fix compilation errors
  patch -Np1 -i ../ar2-ar-fix.patch
  patch -Np1 -i ../ar2-arsup-fix.patch
  patch -Np1 -i ../ar2-lz1-fix.patch
  patch -Np1 -i ../ar2-o2u-c-fix.patch
  patch -Np1 -i ../ar2-o2u-h-fix.patch
  patch -Np1 -i ../mamou-mamou-fix.patch
  
  cd build/unix
  sed -i '/(CC)/ s/$/ $(LDFLAGS)/' ar2/Makefile
  sed -i '/(CC)/ s/$/ $(LDFLAGS)/' makewav/Makefile
}

build() {
  cd "$pkgname-$pkgver"
  make -C build/unix
}

check() {
  cd "$pkgname-$pkgver" 
  tests/hybrid-dsk.sh
  tests/multihdb-dsk.sh
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir/" -C build/unix install

  # Install license file
  sed -n '/Copyright/,/PARTICULAR PURPOSE./p' casm/src/util.h > LICENSE
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE
  
  # Install image for HTML manual
  install -m644 doc/cover.jpg "$pkgdir/usr/share/doc/$pkgname/"
}

# vim:set ts=2 sw=2 et:
