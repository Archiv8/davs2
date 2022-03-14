#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors
# FixMe: endian test failed

# Maintainer : Daniel Bermond < gmail-com: danielbermond >
# Contributor: Ross Clark <contact@artisteducator.com>

# NOTE:
# 10-bit depth currently fails to build
# https://github.com/pkuvcl/davs2/issues/4

pkgname=davs2
pkgver=1.6
pkgrel=7
arch=("x86_64")
pkgdesc="Open-Source decoder of AVS2-P2/IEEE1857.4 video coding standard"
url="https://github.com/pkuvcl/davs2/"
license=("GPL")
depends=(
    # Official Arch Linux repositories
    "glibc"
    )
makedepends=(
    # Official Arch Linux repositories
    "yasm"
    )
provides=(
    "libdavs2"
    )
conflicts=(
    "libdavs2"
    )
replaces=(
    "libdavs2"
)

source=(
    "${pkgname}-${pkgver}.tar.gz"::"https://github.com/pkuvcl/${pkgname}/archive/${pkgver}.tar.gz"
        "davs2-1.6-gcc8-fix.patch"
        )
sha256sums=(
    "de93800f016cbaf08cb40184a8069050dc625da5240a528155137052d1cf81c8"
            "4bea78a55bf6a34591ae016cee800aa75c3c5b1706724534095cf2a0e9fc6e71"
            )

prepare() {
    cd "${pkgname}-${pkgver}"

    patch --binary -Np1 -i "${srcdir}/davs2-1.6-gcc8-fix.patch"
}

build() {
    cd "${pkgname}-${pkgver}/build/linux"

    ./configure \
        --prefix="/usr" \
        --extra-ldflags="-Wl,-z,noexecstack" \
        --enable-shared \
        --disable-static \
        --bit-depth="8" \
        --chroma-format="all" \
        --enable-lto \
        --enable-pic

    make
}

package() {
    make -C "${pkgname}-${pkgver}/build/linux" DESTDIR="$pkgdir" install-cli install-lib-shared
}
