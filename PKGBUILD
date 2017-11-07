pkgname=headunit-desktop-git
pkgver=r118.be7e26b
pkgrel=2
pkgdesc="HeadUnit Desktop is a car PC software built with Qt 5 and QML"
arch=('any')
url="https://github.com/viktorgino/headunit-desktop"
license=('GPL3')
depends=(
  'qt5-base'
  'qt5-multimedia'
  'qt5-quickcontrols'
  'qt5-quickcontrols2'
  'qt5-graphicaleffects'
  'qt-gstreamer'
  'openssl'
  'glib2'
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
  '51-android.rules'
)
sha256sums=(
  'SKIP'
  'ac6ba71fe26d4e8c4f3fb71a085a479fe891b1cb4bd2fd02ce1a120375fdac8b'
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
  install -D -m644 51-android.rules "$pkgdir"/etc/udev/rules.d/51-android.rules
  install -D -m755 "$srcdir/headunit-desktop/headunit-app" "$pkgdir"/usr/bin/headunit-app
}
