# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-pyjwt
pkgname=('python-pyjwt' 'python2-pyjwt')
pkgver=1.6.4
pkgrel=2
pkgdesc='JSON Web Token implementation in Python'
arch=('any')
url='https://github.com/jpadilla/pyjwt'
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'python-pytest-cov' 'python2-pytest-cov')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/jpadilla/pyjwt/archive/$pkgver.tar.gz")
sha512sums=('d6c9ff1c281b00e2a2baf0c916d721ecc0c1bdc51fab73a6be91ac8d603bd448cdb3eebe189201039a3cb8504f3dcee9da73c71bc930c37ce29d99d92287ccb7')

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
