# Maintainer: Luís Ferreira <net dot lsferreira at contact, backwards>
# Contributor: Oscar Shrimpton <oscar.shrimpton.personal@gmail.com>
# Contributor: GI Jack <GI_Jack@hackermail.com>

pkgname=sleuthkit-java
pkgver=4.12.0
pkgrel=1
pkgdesc='Java bindings for The Sleuth Kit.'
arch=(x86_64)
url='http://www.sleuthkit.org/sleuthkit'
license=('CPL', 'custom:"IBM Public Licence"', 'GPL2')
depends=(java-runtime=8 java8-openjfx sleuthkit)
optdepends=('sqlite-jdbc: For JDBC SQLite support')
makedepends=(ant java-environment=8)
source=("https://github.com/sleuthkit/sleuthkit/releases/download/sleuthkit-${pkgver}/sleuthkit-${pkgver}.tar.gz")
sha512sums=('9f20eb42d1dd7d0e15d49a4b6c18441cd31d2343fe34bc7fad1a6b6fe344b414efe959a4f7e34f5368a6efafeecbf39655648a9a3045b437a747c726134c77dc')

build() {
	cd "sleuthkit-${pkgver}"

	# build main program
	aclocal
	automake
	./configure --prefix=/usr
	make

	# build java bindings
	(cd bindings/java;
		ant -q dist
	)

	(cd case-uco/java;
		ant -q
	)

}

package() {
	cd "sleuthkit-${pkgver}"

	install -d "$pkgdir/usr/share/java"
	install -Dm0644 "bindings/java/dist/sleuthkit-${pkgver}.jar" "$pkgdir/usr/share/java"
	install -Dm0644 "case-uco/java/dist/sleuthkit-caseuco-${pkgver}.jar" "$pkgdir/usr/share/java"

	install -d "$pkgdir/usr/lib"
	install -Dm0644 "bindings/java/jni/.libs"/*.so.0.0.0 "$pkgdir/usr/lib"
	ln -s /usr/lib/libtsk_jni.so.0.0.0 "$pkgdir/usr/lib/libtsk_jni.so.0"
	ln -s /usr/lib/libtsk_jni.so.0.0.0 "$pkgdir/usr/lib/libtsk_jni.so"
}
