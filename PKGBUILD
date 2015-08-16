# $Id: PKGBUILD 59857 2011-12-01 12:57:22Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: William Rea <sillywilly@gmail.com>
# Contributor: Benjamin Andresen <benny@klapmuetz.org>
# Contributor: eliott <eliott@cactuswax.net>

pkgname=hula
pkgver=r2661
pkgrel=3
pkgdesc="A calendar and mail server"
arch=('i686' 'x86_64')
url="http://developer.novell.com/wiki/index.php/Hula"
options=('!libtool')
depends=('popt' 'libldap' 'mono' 'perl')
install=$pkgname.install
license=('GPL')
source=(http://archlinux-stuff.googlecode.com/files/hula-$pkgver.tar.gz
	hula-script
	build-fix.patch)
md5sums=('4a50509873ea6bfdeb8daf7540d15d85'
         '6cad58336400ee5d157a1ee4ae150bfd'
         '004c478d9ea9b781b84f67c68f7d89d2')

build() {
  export MONO_SHARED_DIR=$srcdir/.wabi
  mkdir -p $MONO_SHARED_DIR

  cd $srcdir/$pkgname

  sed -i '/CONNECTION_TIMEOUT/s/$/ \n#define VERBOSE_SPAMASSASSIN/' src/agents/antispam/antispam.h
  patch -p1 <$srcdir/build-fix.patch

  unset LDFLAGS

  ./autogen.sh --prefix=/usr
  make
  make DESTDIR=$pkgdir install

  install -D -m755 ../../hula-script $pkgdir/etc/rc.d/hula
  rm -r  $MONO_SHARED_DIR
}
