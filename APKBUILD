pkgname=mariadb-connector-odbc
pkgver=3.0.5
pkgrel=1
pkgdesc="ODBC driver for MariaDB"
url="http://mirror.mephi.ru/mariadb"
arch="all"
license="GPLv2 with exceptions"
depends=""
depends_dev=""
makedepends="$depends_dev mysql-dev unixodbc-dev cmake"
install=""
subpackages=""
source="http://mirror.mephi.ru/mariadb/connector-odbc-${pkgver}/mariadb-connector-odbc-${pkgver}-ga-src.tar.gz"

_builddir="$srcdir"/$pkgname-$pkgver-ga-src
prepare() {
	local i
	cd "$_builddir"
	for i in $source; do
		case $i in
		*.patch) msg $i; patch -p1 -i "$srcdir"/$i || return 1;;
		esac
	done
}

build() {
	cd "$_builddir"
	cmake . -G "Unix Makefiles" \
		-DWITH_UNIXODBC=1 \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DMYSQLCLIENT_LIB_NAME=mysqlclient \
		|| return 1
	make || return 1
}

package() {
	cd "$_builddir"
	make DESTDIR="$pkgdir" install || return 1
	rm -r "$pkgdir"/usr/bin \
		|| return 1

}

sha512sums="f58f135853af89a299d8311bad32df4db2448b49edd34b081de2f76eb11d073ee658bb9792c7a6c40d8b610f522f84d44f1ce5c7d694154b53056e8a85b3a3b5  mariadb-connector-odbc-3.0.5-ga-src.tar.gz"
