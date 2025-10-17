pkgname=qt6-qtquick3d
pkgver=6.10.0
pkgrel=2
pkgdesc="Qt module and API for defining 3D content in Qt Quick"
arch=('x86_64')
url="https://www.qt.io"
license=(
    'GPL-3.0-only'
    'LGPL-3.0-only'
    'LicenseRef-Qt-Commercial'
    'Qt-GPL-exception-1.0'
)
depends=(
    'gcc-libs'
    'glibc'
    'openxr'
    'qt6-qtbase'
    'qt6-qtdeclarative'
    'qt6-qtquicktimeline'
    'qt6-qtshadertools'
    'zlib'
)
makedepends=(
    'assimp'
    'cmake'
    'git'
    'ninja'
    'vulkan-headers'
)
source=(git+https://code.qt.io/qt/${pkgname#*-}#tag=v${pkgver}
    assimp-6.patch)
sha256sums=(86b647b0b728558888a92427de506f473aef63c379818662eb3395cd6ca7cddf
    573f00cdad90d77786fba80066d61d5ee97fc56a8b11d0896949acd16bda8e91)

prepare() {
    cd ${pkgname#*-}

    patch -p1 < ${srcdir}/assimp-6.patch
}

build() {
    cd ${pkgname#*-}

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D INSTALL_LIBDIR=lib64
        -D CMAKE_MESSAGE_LOG_LEVEL=STATUS
    )

    cmake "${cmake_args[@]}"

    cmake --build flarebird-build
}

package() {
    cd ${pkgname#*-}

    DESTDIR=${pkgdir} cmake --install flarebird-build
}
