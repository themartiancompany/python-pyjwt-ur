# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-pyjwt
pkgname=('python-pyjwt' 'python2-pyjwt')
pkgver=1.5.3
pkgrel=1
pkgdesc='JSON Web Token implementation in Python'
arch=('any')
url='https://github.com/jpadilla/pyjwt'
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'python-pytest-cov' 'python2-pytest-cov')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/jpadilla/pyjwt/archive/$pkgver.tar.gz")
sha512sums=('eeb655a739cb32878f53809fb6206cabb33c2767c3d34f923228cabe3282e3791a689d6a15374626559a22c270dbb88bbe0a74d8236a82987dc613473d38b845')

prepare() {
  sed -i 's/pytest==2.7.3/pytest/' pyjwt-$pkgver/setup.py
  cp -a pyjwt-$pkgver{,-py2}
}

build() {
  cd "$srcdir"/pyjwt-$pkgver
  python setup.py build

  cd "$srcdir"/pyjwt-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/pyjwt-$pkgver
  python setup.py pytest

  cd "$srcdir"/pyjwt-$pkgver-py2
  python2 setup.py pytest || warning "Tests failed"
}

package_python-pyjwt() {
  depends=('python-setuptools')

  cd pyjwt-$pkgver
  python3 setup.py install --root="$pkgdir" -O1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-pyjwt() {
  depends=('python2-setuptools')

  cd pyjwt-$pkgver-py2
  python2 setup.py install --root="$pkgdir" -O1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE

  mv "$pkgdir"/usr/bin/pyjwt{,2}
}
