# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname=n3n
pkgver=3.3.2
pkgrel=1
epoch=
pkgdesc="Peer to Peer VPN"
arch=(i686 x86_64 armv7h aarch64)
url="https://github.com/n42n/n3n"
license=('GPL2' 'GPL3' 'LGPL2.1')
groups=()
depends=('libcap' 'openssl' 'miniupnpc' 'zstd')
makedepends=('libpcap')
checkdepends=()
optdepends=('libpcap: for n3n-decode')
provides=()
conflicts=()
replaces=()
backup=('etc/n3n/edge.conf'
        'etc/n3n/supernode.conf')
options=()
install=
changelog=
source=("https://github.com/n42n/n3n/archive/refs/tags/$pkgver.tar.gz")
noextract=()
sha256sums=('24c5209abe81f591009a3be062ece803c018715c3b75929cc921a3e7455f3381')
validpgpkeys=()

prepare() {
	cd "$pkgname-$pkgver"
	sed -i 's|/sbin|/bin|' Makefile
	sed -i 's|/usr/sbin|/usr/bin|' packages/lib/systemd/system/*.service
}

build() {
	cd "$pkgname-$pkgver"
	echo "$PWD"
	./autogen.sh
	./configure \
		--with-zstd \
		--with-openssl \
		--enable-miniupnp \
		--enable-pcap \
		--enable-cap \
		--enable-pthread \
		--prefix=/usr
	make
}

check() {
	cd "$pkgname-$pkgver"
}

package() {
	cd "$pkgname-$pkgver"
	DESTDIR="$pkgdir" SBINDIR="$pkgdir"/usr/bin make install
	
	install -Dm644 doc/edge.conf.sample "$pkgdir"/etc/n3n/edge.conf
	install -Dm644 doc/supernode.conf.sample "$pkgdir"/etc/n3n/supernode.conf
	make DESTDIR="$pkgdir/" install
}
