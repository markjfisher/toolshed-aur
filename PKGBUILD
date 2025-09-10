# Maintainer: Paul Hentschel <aur at hpminc dot com>

pkgname=toolshed
pkgver=v2_4_1.r2.g296e93a
pkgrel=1
pkgdesc="Utilities for Tandy Color Computer and Dragon microcomputers cross-development."
arch=('x86_64')
url="https://github.com/nitros9project/toolshed"
license=('PerlArtistic')
depends=('fuse2')
makedepends=('discount' 'git')
source=("git+https://github.com/nitros9project/toolshed.git")
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  # Use git describe to get version with commit count and hash
  # This gives us: v2_4_1-2-g296e93a -> v2_4_1.r2.g296e93a
  git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$pkgname"
  
  # Fetch tags for git describe to work
  git fetch --tags
}

build() {
  cd "$pkgname"
  make -C build/unix
}

check() {
  cd "$pkgname" 
  tests/hybrid-dsk.sh
  tests/multihdb-dsk.sh
}

package() {
  cd "$pkgname"
  make DESTDIR="$pkgdir/" -C build/unix install

  # Install license file
  sed -n '/Copyright/,/PARTICULAR PURPOSE./p' casm/src/util.h > LICENSE
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" LICENSE
  
  # Install image for HTML manual
  install -m644 doc/cover.jpg "$pkgdir/usr/share/doc/$pkgname/"
}

# vim:set ts=2 sw=2 et:
