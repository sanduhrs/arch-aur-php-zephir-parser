# Maintainer: wolftankk <wolftankk@gmail.com>
pkgname=php-zephir-parser
pkgver=1.3.1
pkgrel=1
pkgdesc="The Zephir Parser delivered as a C extension for the PHP language."
url="https://github.com/phalcon/php-zephir-parser"
arch=('x86_64' 'i686')
license=('MIT')
depends=('re2c')
makedepends=('php>=5.5' 'gcc' 'pcre' 'autoconf')
backup=('etc/php/conf.d/php-zephir.ini')

if [[ $CARCH = "i686" ]]; then
  makedepends+=('lib32-pcre');
fi

source=(
    "https://github.com/phalcon/php-zephir-parser/archive/v${pkgver}.tar.gz"
)

sha256sums=('1e54b0ddc6b99510bcb2cfa3c235473a9c1bba40c4a1a977e22298a39698d621')

#get php version
PHP_FULL_VERSION=`php-config --version`
if [ "${PHP_FULL_VERSION:0:1}" == "5" ]; then
    PHP_VERSION="php5"
else
    PHP_VERSION="php7"
fi

#build zephir-parser
build() {
  cd "$srcdir/php-zephir-parser-$pkgver"
  if [ -f Makefile ]; then
      make clean
      phpize --clean
  fi

  phpize
  ./configure --prefix=/usr --enable-zephir_parser

  make -s -j2
}

package() {
  cd "$srcdir/php-zephir-parser-$pkgver"

  make INSTALL_ROOT="$pkgdir" install
  echo 'extension=zephir_parser.so' > zephir_parser.ini 
  install -Dm644 zephir_parser.ini "$pkgdir/etc/php/conf.d/zephir_parser.ini"
}
