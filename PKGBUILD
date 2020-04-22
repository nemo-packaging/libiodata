# $Id$
# Contributor: TheKit <nekit1000 at gmail.com>
# Contributor: Bart Ribbers <bribbers@disroot.org>
# Contributor: Alexey Andreyev <aa13q@ya.ru>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

_host="git.sailfishos.org"
_project=mer-core
_basename=iodata
_branch=master

_gitname=lib${_basename}
pkgname=qt5-$_basename-git

pkgver=0.19.11.r0.gd13b7d8

pkgrel=1
pkgdesc="Mer library for input/output data"
arch=('x86_64' 'aarch64')
url="https://$_host/$_project/$_gitname#branch=$_branch"
license=('LGPL-2.1-or-later')
depends=('qt5-base' 'dbus')
makedepends=('git' 'bison' 'flex')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=("${pkgname}::git+${url}")
md5sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  ( set -o pipefail
    git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  ) 2>/dev/null
}

prepare() {
  cd "${srcdir}/${pkgname}"
  # Logging macro cause compilation to fail otherwise
  sed -i "s@define LOG_LEVEL LOG_WARNING@define LOG_LEVEL LOG_NONE@" src/log.h
}

build() {
  cd "${srcdir}/${pkgname}"
  export IODATA_VERSION=0.19.10
  qmake
  make -j1
}

package() {
  cd "${srcdir}/${pkgname}"
  make INSTALL_ROOT="${pkgdir}" install
}
