# Maintainer: SummerSad

pkgname=st
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple terminal implementation for X with patches'
arch=('x86_64')
license=('MIT')
url="https://st.suckless.org/"
depends=('libxft')
makedepends=('ncurses')
_patches=(
	"https://st.suckless.org/patches/clipboard/st-clipboard-$pkgver.diff"
	"font.patch"
	"color.patch"
)
source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "${_patches[@]}")
md5sums=('92135aecdba29300bb2e274a55f5b71e'
         'd7295edae3ff61b93e9f875f6eaaad7a'
         'f39726d6394805f9c095bf90f4b45987'
         '6f8a863906ba8dd84dedd5d322cfd9ec')

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
