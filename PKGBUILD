# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=git-sv
pkgver=2.0.7 # renovate: datasource=github-releases depName=thegeeklab/git-sv extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="Semantic versioning tool for git based on conventional commits "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/thegeeklab/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('de7ff2817b25e88c9d6b2c054a7bafe6d234bd0b44135d1264d1d42c46465bbe03765af2380de571bdb52b0737e7e3c487061814bad3314e32c95ddc9e1f475c')
b2sums=('8b1847602b333632128d0e2a4fbb379221f9d6f322bb6afb4c6405af88485f2f5d404f2445ed2c8b2b97c63df81b5dd451e5e104b15e8bfdbe5d61e017cbc450')

build() {
  make --directory "$pkgname-$pkgver" build
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/dist/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
