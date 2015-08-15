# Maintainer: N30N <archlinux@alunamation.com>
# Contributer: mrbit <giacomogiorgianni@gmail.com>

pkgname=gsculpt
pkgver=0.99.47
pkgrel=2
pkgdesc="A procedural 3D modelling application with a comprehensive set of \
	polygon mesh editing tools."
url="http://gsculpt.sourceforge.net"
license="GPL2"
arch=("i686" "x86_64")
depends=("boost" "python-gtkglext" "python2-imaging")
makedepends=("scons")
source=("http://downloads.sourceforge.net/${pkgname}/gSculpt-${pkgver}-alpha-src.tar.gz" \
	"gsculpt.desktop")
sha256sums=("cb7f0cbff996da66318ab0e2e9bd5f5ebf1170ab9daa4b504e6fc68736d7bc30" \
	"c2bafd2108c9a920bc3acd2cd2277f46ad3a3ed1db3f18907cd3f07e0e21720a")


build() {
	cd gSculpt-${pkgver}-alpha

	sed 10a"#include <cstdio>" -i cpp/Math/Vector2.h
	sed -r "s/^(cppLibs.*)BackgroundModel/\1BackgroundMesh/" -i SConstruct
	sed -r \
		-e "s|^(prefix = ).*|\1\"${pkgdir}/usr\"|" \
		-e "s|^(gSculptStartDir = ).*|\1\"${pkgdir}/usr/lib/gSculpt\"|" \
		-i SConstruct-install
	sed -e "s/python/python2/" \
		-e "s|#GSCULPT_LIBRARY_PATH#|/usr/lib/gSculpt|" \
		-e "s|#GSCULPT_START#|/usr/lib/gSculpt/gsculpt.py|" \
		-i posixbuild/gsculpt
	sed "s/, '-Werror'//" -i SConstruct

	scons
}

package () {
	cd gSculpt-${pkgver}-alpha

	scons -f SConstruct-install -Q install

	install -D -m755 posixbuild/gsculpt ${pkgdir}/usr/bin/gsculpt
	install -D -m644 ${srcdir}/gsculpt.desktop \
		${pkgdir}/usr/share/applications/gsculpt.desktop
}

# vim: set noet ff=unix
