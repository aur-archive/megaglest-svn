# Maintainer: Kiodo1981 <cristianmartina1981@gmail.com>

pkgname=megaglest-svn
pkgver=2858
pkgrel=1
pkgdesc="Fork of Glest, a 3D real-time strategy game in a fantastic world."
url="http://megaglest.org/"
arch=('i686' 'x86_64')
license=('GPL')
depends=('lua' 'mesa' 'wxgtk' 'xerces-c' 'glew' 'ftgl' 'libvorbis' 'zlib' 'freetype2')
makedepends=('cmake' 'svn')

_svntrunk=https://megaglest.svn.sourceforge.net/svnroot/megaglest/trunk
_svnmod=megaglest_svn

build() {
	cd "$srcdir"

	if [ -d $_svnmod/.svn ]; then
		(cd $_svnmod && svn up -r $pkgver)
	else
		svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
	fi

	msg "SVN checkout done or server timeout"
	msg "Starting make..."
	
	rm -rf build
	mkdir -p build
	cd build
	cmake -DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_INSTALL_PREFIX=/usr \
		"$srcdir/$_svnmod" || return 1
	make || return 1
	make DESTDIR=${pkgdir} install || return 1
}
