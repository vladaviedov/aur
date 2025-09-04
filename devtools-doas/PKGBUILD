# Maintainer: Vladyslav Aviedov <aur at vladaviedov dot org>
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Christian Heusel <gromit@archlinux.org>
# Contributor: Pierre Schmitz <pierre@archlinux.de>

_orig_pkgname=devtools
pkgname=devtools-doas
epoch=1
pkgver=1.3.2
pkgrel=1
pkgdesc='Tools for Arch Linux package maintainers (patched for opendoas)'
arch=('any')
license=('GPL-3.0-or-later')
url='https://gitlab.archlinux.org/archlinux/devtools'
depends=(
  arch-install-scripts
  awk
  bash
  binutils
  coreutils
  curl
  diffutils
  expac
  fakeroot
  findutils
  glow
  grep
  gum
  jq
  openssh
  parallel
  rsync
  sed
  util-linux

  breezy
  git
  mercurial
  subversion

  opendoas
)
makedepends=(
  asciidoctor
  shellcheck
)
checkdepends=(
  bats
)
provides=('devtools')
conflicts=('devtools')
optdepends=(
  'btrfs-progs: btrfs support'
  'bat: pretty printing for pkgctl search'
  'nvchecker: pkgctl version subcommand'
)
replaces=(devtools-git-poc)
source=(
  https://gitlab.archlinux.org/archlinux/devtools/-/releases/v${pkgver}/downloads/devtools-${pkgver}.tar.gz{,.sig}
  doas.patch
)
# Import a key from the main devtools package
# https://gitlab.archlinux.org/archlinux/packaging/packages/devtools/-/tree/main/keys/pgp
validpgpkeys=(
  'E240B57E2C4630BA768E2F26FC1B547C8D8172C8' # Levente Polyak <anthraxx@archlinux.org>
  'F00B96D15228013FFC9C9D0393B11DAA4C197E3D' # Christian Heusel (gromit packager key) <gromit@archlinux.org>
)
sha256sums=('9dc7cd3743c5669494e344ec99b1cd2a5b55cfadcbdbe97bd9f5761e72905964'
            'SKIP'
            'SKIP')
b2sums=('e649eccb4242d568dd4659e7ad7d3c88ac6e34913bd9df82776012031e54d62ad76223bdd9bdfb4df694df968ff49fc558109855678d99edac4203ddd4cda4fc'
        'SKIP'
        'SKIP')
install=devtools.install

build() {
  mv ${_orig_pkgname}-${pkgver} ${pkgname}-${pkgver}
  cd ${pkgname}-${pkgver}
  patch -Np1 -i ../doas.patch
  make BUILDTOOLVER="${epoch}:${pkgver}-${pkgrel}-${arch}" PREFIX=/usr
}

check() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr test
}

package() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" install
}

# vim: ts=2 sw=2 et:
