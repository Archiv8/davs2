#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

# NOTE:
# 10-bit depth currently fails to build
# https://github.com/pkuvcl/davs2/issues/4

pkgname=davs2
pkgver=1.7
pkgrel=1
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
    "nasm"
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
options=("!lto")
source=(
    "${pkgname}-${pkgver}.tar.gz"::"https://github.com/pkuvcl/${pkgname}/archive/${pkgver}.tar.gz"
)
sha512sums=(
    "273ec948a045941ed4fda0191cdffc821ded225a89f0d0c9408fea86ae61202a9fc9f41d601a95cc18a4f2a93a81d0fcb1e6c5e70a3d334e76a9e309abbc5f55"
)

# prepare() {
#
# }

build() {

    cd "${pkgname}-${pkgver}/build/linux"

    ./configure \
        --prefix="/usr" \
        --extra-ldflags='-Wl,-z,noexecstack' \
        --enable-shared \
        --disable-static \
        --bit-depth="8" \
        --chroma-format="all" \
        --enable-pic

    make
}

package() {
    make -C "${pkgname}-${pkgver}/build/linux" DESTDIR="$pkgdir" install-cli install-lib-shared
}
