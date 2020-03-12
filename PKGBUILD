# $Id$
# Maintainer: TheKit <nekit1000 at gmail.com>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

_pkgname=libiodata
pkgname=libiodata-git
pkgver=0.19.10+git2.r0.ga7f5448
pkgrel=1
pkgdesc="Mer library for input/output data"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/mer-core/libiodata"
license=('GPL')
depends=('qt5-base' 'dbus')
makedepends=('git' 'bison' 'flex')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=('git+https://git.sailfishos.org/mer-core/libiodata.git')
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/$_pkgname"
	# Logging macro cause compilation to fail otherwise
    sed -i "s@define LOG_LEVEL LOG_WARNING@define LOG_LEVEL LOG_NONE@" src/log.h
}

build() {
	cd "$srcdir/$_pkgname"
    export IODATA_VERSION=0.19.10
    qmake
    make -j1
}

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir/" install
}
