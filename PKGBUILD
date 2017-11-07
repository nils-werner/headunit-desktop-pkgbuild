pkgname=headunit-desktop-git
pkgver=r118.be7e26b
pkgrel=1
pkgdesc="HeadUnit Desktop is a car PC software built with Qt 5 and QML"
arch=('any')
url="https://github.com/viktorgino/headunit-desktop"
license=('GPL3')
depends=(
  'qt5-base'
  'qt5-multimedia'
  'qt-gstreamer'
  'openssl'
  'libusb'
  'protobuf'
  'libunwind'
  'gst-plugins-bad'
  'gst-plugins-base'
  'gst-libav'
  'boost'
)
source=(
  'git+https://github.com/viktorgino/headunit-desktop.git'
)
sha256sums=(
  'SKIP'
)

pkgver() {
  cd "$srcdir/headunit-desktop"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "$srcdir/headunit-desktop"
  git submodule update --init --recursive
}

build() {
  cd "$srcdir/headunit-desktop"
  protoc --proto_path=headunit/hu/ --cpp_out=headunit/hu/generated.x64/ headunit/hu/hu.proto
  qmake PREFIX="/usr"
  make sub-app-pro
}

package() {
  cd "$srcdir/headunit-desktop"
  make INSTALL_ROOT="$pkgdir" install
}
