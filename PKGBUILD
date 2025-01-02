# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Felix Yan <felixonmars@archlinux.org>

pkgname=python-pyjwt
pkgver=2.10.1
pkgrel=1
pkgdesc='JSON Web Token implementation in Python'
arch=(any)
url=https://github.com/jpadilla/pyjwt
license=(MIT)
depends=(python)
makedepends=(
  git
  python-build
  python-installer
  python-setuptools
  python-wheel
)
checkdepends=(
  python-cryptography
  python-pytest
)
_tag=3ebbb22f30f2b1b41727b269a08b427e9a85d6bb
source=(git+https://github.com/jpadilla/pyjwt.git#tag=${_tag})
b2sums=('729bd24956fdae22be95c9d19be89a801dc9b3c20967a9c3ff737530040f68c20a3fa304b5337ad2046562a957fd4b17fba98587d03471c4f310f4da2b53fb14')

pkgver() {
  cd pyjwt
  git describe --tags
}

build() {
  cd pyjwt
  python -m build -wn
}

check() {
  cd pyjwt
  pytest
}

package() {
  python -m installer -d "${pkgdir}" pyjwt/dist/*.whl
  install -Dm 644 pyjwt/LICENSE -t "${pkgdir}"/usr/share/licenses/python-pyjwt/
}

# vim: ts=2 sw=2 et:
