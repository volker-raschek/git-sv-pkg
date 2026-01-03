# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=git-sv
pkgver=2.0.9 # renovate: datasource=github-releases depName=thegeeklab/git-sv extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="Semantic versioning tool for git based on conventional commits "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/thegeeklab/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('060f5fc91356ce82a3f31c2de5d84f35e27eca45977a77207be2b1d5e116781cfadecd86394739aaa52b2cc9e43a7535929aceed33eca7205e798618e049b817')
b2sums=('711a78ccb3f3cf4d9438cd1461e04809f40f65db7145f4e921cbcfc9ab50447aab633d3e78f894b5f2e83c3bf3987b9ba060891d0918739a3c8486fd68f8da7b')

prepare() {
  cd ${pkgname}-${pkgver}

  export GONOSUMDB="${GONOSUMDB}"
  export GOPATH="${srcdir}"
  export GOPROXY="${GOPROXY}"

  env | sort | grep -E '^C?GO'

  go mod download -modcacherw
}

build() {
  cd "$pkgname-$pkgver/cmd/$pkgname"

  # https://wiki.archlinux.org/title/Go_package_guidelines
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"

  export GONOSUMDB="${GONOSUMDB}"
  export GOPATH="${srcdir}"
  export GOPROXY="${GOPROXY}"

  env | sort | grep -E '^C?GO'

  go build -v \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "\
      -linkmode external \
      -extldflags \"${LDFLAGS}\"
      -X "main.BuildVersion=$pkgver" \
      -X "main.BuildDate=$(date --iso-8601=seconds)"
    " \
    -o $pkgname \
    .
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/cmd/$pkgname/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
