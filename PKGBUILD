# Maintainer: kuri <sysegv@gmail.com>
# Contributor: chefpeyo <pierre-olivier.huguet@asp64.com>

pkgname=libshotgun-svn
pkgver=77727
pkgrel=1
pkgdesc="Shotgun is an xmpp client/library which uses EFL. This package will only build the library"
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL2.1')
depends=('eina-svn' 'ecore')
provides=('libshotgun')
makedepends=('subversion')
optdepends=()
options=('!libtool')
source=()
md5sums=()

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/PROTO/shotgun"
_svnmod="shotgun"

build() {
  cd $srcdir

  if [ $NOEXTRACT -eq 0 ]; then
    msg "Connecting to $_svntrunk SVN server...."
    if [ -d $_svnmod/.svn ]; then
      (cd $_svnmod && svn up -r $pkgver)
    else
      svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
    fi

    msg "SVN checkout done or server timeout"
    msg "Starting make..."

  fi
  cp -r $_svnmod $_svnmod-build
  cd $_svnmod-build

  ./autogen.sh --prefix=/usr --disable-gui
  make || return 1
  make DESTDIR=$pkgdir install || return 1

# install license files
  install -Dm644 $srcdir/$_svnmod-build/COPYING \
  	$pkgdir/usr/share/licenses/$pkgname/COPYING

  rm -r $startdir/src/$_svnmod-build
}
