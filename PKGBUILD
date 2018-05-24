# Maintainer: SummerSad <hauvipapro@gmail.com>

pkgname=st
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple terminal implementation for X with patches.'
arch=('x86_64')
license=('MIT')
url="https://st.suckless.org/"
depends=('libxft')
makedepends=('ncurses')
_patches=(
	"https://st.suckless.org/patches/clipboard/st-clipboard-$pkgver.diff"
	"https://st.suckless.org/patches/scrollback/st-scrollback-0.8.diff"
	"https://st.suckless.org/patches/scrollback/st-scrollback-mouse-0.8.diff"
	"theme.patch"
)
source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "${_patches[@]}")
sha256sums=('c4fb0fe2b8d2d3bd5e72763e80a8ae05b7d44dbac8f8e3bb18ef0161c7266926'
            'f22e0165aacb2bc86d000728c81f68022abcc601dbfd09e516e1ba772225d7e6'
            '8279d347c70bc9b36f450ba15e1fd9ff62eedf49ce9258c35d7f1cfe38cca226'
            '3fb38940cc3bad3f9cd1e2a0796ebd0e48950a07860ecf8523a5afd0cd1b5a44'
            '05816e2a5d1419544136596f619dade0298232e80b23f4c18354da88147a4ee8')

prepare() {
	cd $srcdir/$pkgname-$pkgver
	# skip terminfo which conflicts with nsurses
	sed -i '/tic /d' Makefile
	# patch
	for file in "${_patches[@]}"; do
		if [[ "$file" == *.diff || "$file" == *.patch ]]; then
			echo "Applying patch $(basename $file)..."
			patch -Np1 <"$srcdir/$(basename ${file})"
		fi
	done
}

build() {
	cd $srcdir/$pkgname-$pkgver
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd $srcdir/$pkgname-$pkgver
	make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
