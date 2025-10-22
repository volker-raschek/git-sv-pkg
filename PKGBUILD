# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=git-sv
pkgver=2.0.2 # renovate: datasource=github-releases depName=thegeeklab/git-sv extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="Semantic versioning tool for git based on conventional commits "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/thegeeklab/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('2bb40ff8f4ccaded79daa0406ad84a85e75b5a36bf42b5220b7bcbbf990224ff8c7c8927766acda32572f249dedb6d0cac34850853451a8f063d7039a28a33e4')
b2sums=('7633f33ef6f266e93426e212750f178108ea3925162efc7a8758ce816467ff9d0e477a37db6fcccb5360f53e93f086bd23230c42ac0e36cfcd86f7fc1e4d97d3')

build() {
  make --directory "$pkgname-$pkgver" build
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/cmd/$pkgname/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
