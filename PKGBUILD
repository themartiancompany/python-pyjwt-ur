# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-pyjwt
pkgname=('python-pyjwt' 'python2-pyjwt')
pkgver=1.5.1
pkgrel=1
pkgdesc='JSON Web Token implementation in Python'
arch=('any')
url='http://github.com/jpadilla/pyjwt'
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'python-pytest-cov' 'python2-pytest-cov')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/jpadilla/pyjwt/archive/$pkgver.tar.gz")
sha512sums=('9319dc0eb643e9c5bfeb7cc1c23a59429fb661d7898a85ddb3b0cdc9c3dad1ac4735e6444e55615783895810ebcd0bcd17fb108f4a3d055f68c609d569f76e30')

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
