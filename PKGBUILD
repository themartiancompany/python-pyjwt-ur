# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-pyjwt
pkgname=('python-pyjwt' 'python2-pyjwt')
pkgver=1.5.0
pkgrel=1
pkgdesc='JSON Web Token implementation in Python'
arch=('any')
url='http://github.com/jpadilla/pyjwt'
license=('MIT')
makedepends=('python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'python-pytest-cov' 'python2-pytest-cov')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/jpadilla/pyjwt/archive/$pkgver.tar.gz")
sha512sums=('1b5c0d558605b755b95eb2c2d34f467756cae81c67a1f2b47096bf513f669d93d85f4a16fa11e5a3630525497e5c86e424a161d4d834aed1270549a1715c0672')

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
