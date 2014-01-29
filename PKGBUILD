# Maintainer: Doug Elkin <drelkin86@gmail.com>
_pkgname='markdowner'
pkgname="$_pkgname-bzr"
pkgver=11
pkgrel=2
pkgdesc="Markdowner is a simple markdown editor that will allow a user to write markdown text and view the parsed HTML output."
arch=(any)
url="http://www.jezra.net/projects/${_pkgname}"
license=('GPL3')
depends=('python2' 'gtk2' 'libwebkit' 'python2-markdown' 'pywebkitgtk')
optdepends=('python2-gtkspell: spellcheck support')
makedepends=('bzr')
provides=('markdowner')
source=('markdowner.desktop')
sha256sums=('1544f0d6b1939657588c587fa3578cad4b5ba8fa349ed270bb16aa0c1982169b')

_bzrtrunk="https://code.launchpad.net/~jezra/${_pkgname}/trunk"
_bzrmod=$_pkgname

build() {
  cd "$srcdir"
  msg "Connecting to Bazaar server...."

  if [[ -d "$_bzrmod" ]]; then
    cd "$_bzrmod" && bzr --no-plugins pull "$_bzrtrunk" -r "$pkgver"
    msg "The local files are updated."
  else
    bzr --no-plugins branch "$_bzrtrunk" "$_bzrmod" -q -r "$pkgver"
  fi

  msg "Bazaar checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_bzrmod-build"
  cp -r "$srcdir/$_bzrmod" "$srcdir/$_bzrmod-build"
  cd "$srcdir/$_bzrmod-build"

}

package() {
  cd "$srcdir/$_bzrmod-build"
  sed -i 1s+python+python2+ "markdowner.py"
  install -Dm755 markdowner.py "${pkgdir}/usr/bin/markdowner"
  install -Dm755 icon.png "${pkgdir}/usr/share/icons/markdowner.png"
  install -Dm755 ../markdowner.desktop "${pkgdir}/usr/share/applications/markdowner.desktop"
}

# vim:set ts=2 sw=2 et:
