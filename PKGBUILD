# Maintainer: Jguer <pkgbuilds at jguer.space>
pkgname=yay
pkgver=12.0.2
pkgrel=1
pkgdesc="Yet another yogurt. Pacman wrapper and AUR helper written in go."
arch=('i686' 'pentium4' 'x86_64' 'arm' 'armv7h' 'armv6h' 'aarch64')
url="https://github.com/Jguer/yay"
options=(!lto)
license=('GPL3')
depends=(
  'pacman>5'
  'git'
)
optdepends=(
  'sudo: privilege elevation'
  'doas: privilege elevation'
)
makedepends=(
  'go'
)
options=(!lto)
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/Jguer/yay/archive/v${pkgver}.tar.gz")
sha256sums=('cdf558f351f3b40092a5a52ac6382f2363dd8a6f59a00e9caa12df11a78a80ea')

# With pacman 6 arriving a rebuild of yay will be necessary, if you upgrade pacman without upgrading yay at the same time, yay will not run after.
# I'm bumping the pkgrel so it shows up on the upgrade list (and will do so when pacman transitions from staging->core)
# In case you end up with a non-functioning yay after the upgrade follow the
# instructions on the github page

build() {
  export GOPATH="$srcdir"/gopath
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export CGO_ENABLED=1
  export EXTRA_FLAGS="-buildmode=pie -buildvcs=false"

  cd "$srcdir/$pkgname-$pkgver"
  make VERSION=$pkgver DESTDIR="$pkgdir" PREFIX="/usr" build
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make VERSION=$pkgver DESTDIR="$pkgdir" PREFIX="/usr" install
}
