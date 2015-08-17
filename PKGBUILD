# Maintainer: HitomiTenshi <Johann.Rekowski@googlemail.com>

pkgname=utvideo-git
pkgver=13.0.1_53_970faa1
pkgrel=1
pkgdesc="utvideo with patches for the buildsystem"
arch=('i686' 'x86_64')
url="https://github.com/qyot27/libutvideo"
license=('GPL')
makedepends=('git' 'nasm') # nasm is needed if you compile with --enable-asm
conflicts=('utvideo' 'utvideo-git' 'libutvideo')

source=('utvideo::git://github.com/qyot27/libutvideo.git#branch=buildsystem')
md5sums=('SKIP')
_gitname="utvideo"

pkgver() {
  cd $_gitname
  echo $(git tag -l | tail -1 |tr -d v)_$(git rev-list buildsystem | sort | wc -l | awk '{print $1}')_$(git rev-list HEAD -n 1 --abbrev-commit)
}

build() {
  cd $_gitname

  #configure shared library with asm optimizations for x64.
  [ "${CARCH}" = "i686" ] && _asm="x86"
  [ "${CARCH}" = "x86_64" ] && _asm="x64"

  ./configure \
  --prefix=/usr \
  --enable-shared \
  --disable-static \
  --optlevel=3 \
  --enable-pic
  #--enable-asm="$_asm"
  #There currently is a bug with asm optimizations, causing a segmentation fault when trying to output something.
  #Use this only if you are sure what you're doing.

  make
}

package() {
cd $_gitname
  make DESTDIR=$pkgdir install
}