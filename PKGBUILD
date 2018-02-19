pkgname=st
pkgver=0.7
pkgrel=1
pkgdesc='A simple terminal implementation for X with patches'
arch=('x86_64')
license=('MIT')
url="https://st.suckless.org/"
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
_patches=(
        "https://st.suckless.org/patches/clipboard/st-clipboard-0.7.diff"
        "font.patch"
        "color.patch"
)
source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "${_patches[@]}")
md5sums=('29b2a599cf1511c8062ed8f025c84c63'
         '831b8bdc34b48a3290e39ac9aca2906f'
         '885aae4cd3e6c09aaa9616ff7a2c472e'
         'b11fa0335ffe8a86f077677de7b6e13f')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/\@tic /d' Makefile

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
