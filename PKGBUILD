pkgname=maliit-framework-qt6
pkgver=2.3.0
pkgrel=3
pkgdesc="Framework for Maliit"
arch=('aarch64' 'x86_64')
url="https://github.com/maliit/framework"
license=('LGPL')
depends=('qt6-declarative' 'wayland-protocols' 'qt6-wayland')
makedepends=('git' 'cmake' 'doxygen' 'graphviz' 'glib2-devel' 'extra-cmake-modules')
conflicts=("maliit-framework")
source=("${url}/archive/refs/tags/$pkgver.tar.gz"
    "0001-qt6-v2.patch"
    "0002-qt6-wayland.patch"
    "0003-misc.patch"
    "86e55980e3025678882cb9c4c78614f86cdc1f04.patch")
sha256sums=('bfc23919ac8b960243f85e8228ad7dfc28d557b52182a0b5a2a216a5c6a8057c'
    '566c11ad572a8e31511098c17fa10dac0c2fb75b811540c78156bf664e4863fd'
    'fc224b1bf0e9ee192d3dcbc51aad2f42405860097a62219c44bfd796d0606c75'
    '331dbfc1852e190771a4422b211adf49a7180c3bf89f781e3fc54e59ceabd9cb'
    '396c1b60f9b21a7e770cf40b80a5b6762077eacc02ce545878dbb180359e034e')

prepare() {
    cd framework-$pkgver
    patch -p1 --input="${srcdir}/0001-qt6-v2.patch"
    patch -p1 --input="${srcdir}/0002-qt6-wayland.patch"
    patch -p1 --input="${srcdir}/0003-misc.patch"
    patch -p1 --input="${srcdir}/86e55980e3025678882cb9c4c78614f86cdc1f04.patch"
    mkdir -p build
}

build() {
    cd framework-$pkgver/build
    cmake ../ \
    -DQtWaylandScanner_EXECUTABLE:FILEPATH=/usr/lib/qt6/qtwaylandscanner \
    -DCMAKE_INSTALL_LIBEXECDIR=lib \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DLIB_INSTALL_DIR=lib \
    -Denable-dbus-activation=ON \
    -Denable-docs=OFF \
    -Denable-tests=OFF \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_WITH_QT6=ON
    make
}

package() {
    cd framework-$pkgver/build
    make DESTDIR="$pkgdir/" install
    rm -f $pkgdir/usr/share/dbus-1/services/org.maliit.server.service
}
