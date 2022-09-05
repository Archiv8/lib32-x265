#!/bin/bash

# Created from the original package by

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors



# $Id$
# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: kfgz <kfgz@interia.pl>
# Mantainer: Lorenzo Ferrillo <lorenzofer at live dot it>

_relname=x265
pkgname=lib32-x265
pkgver=3.5
pkgrel=1
pkgdesc='Open Source H265/HEVC video encoder. 32bit libraries.'
arch=('x86_64')
url='https://bitbucket.org/multicoreware/x265_git'
license=('GPL')
depends=(
  'x265' 
  'lib32-gcc-libs'  
  'lib32-libnuma'
  )
makedepends=(
  'git' 
  'cmake' 
  'nasm')
provides=('libx265.so')
source=(
  "https://bitbucket.org/multicoreware/x265_git/downloads/x265_${pkgver}.tar.gz"
  )
sha256sums=(
  'e70a3335cacacbba0b3a20ec6fecd6783932288ebc8163ad74bcc9606477cae8'
  )

# prepare() {
#  cd x265_${pkgver}
#
#  for d in 8 10 12; do
#    if [[ -d build-$d ]]; then
#      rm -rf build-$d
#    fi
#    mkdir build-$d
#  done
# }

build() {
#  cd x265_${pkgver}/build-12
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cmake -S x265_3.5/source -B build-12 \
    -DCMAKE_INSTALL_PREFIX='/usr' -DLIB_INSTALL_DIR='lib32' \
    -DCMAKE_LIBRARY_PATH='/usr/lib32' \
    -DDETAILED_CU_STATS='OFF' \
    -DENABLE_AGGRESSIVE_CHECKS='OFF' \
    -DENABLE_ASSEMBLY='ON' \
    -DENABLE_CLI='ON' \
    -DENABLE_HDR12_PLUS='OFF' \
    -DENABLE_LIBNUMA='ON' \
    -DENABLE_LIBVMAF='OFF' \
    -DENABLE_PIC='ON' \
    -DENABLE_PPA='OFF' \
    -DENABLE_SHARED='ON' \
    -DENABLE_SVT_HEVC='OFF' \
    -DENABLE_TESTS='OFF' \
    -DENABLE_VTUNE='OFF' \
    -DEXPORT_C_API='ON' \
    -DEXTRA_LINK_FLAGS='-L .' \
    -DHIGH_BIT_DEPTH='OFF' \
    -DMAIN12='ON' \
    -Wno-dev
  make -C build-12

  cmake -S x265_3.5/source -B build-10 \
    -DCMAKE_INSTALL_PREFIX='/usr' -DLIB_INSTALL_DIR='lib32' \
    -DCMAKE_LIBRARY_PATH='/usr/lib32' \
    -DDETAILED_CU_STATS='OFF' \
    -DENABLE_AGGRESSIVE_CHECKS='OFF' \
    -DENABLE_ASSEMBLY='ON' \
    -DEXPORT_C_API='ON' \
    -DENABLE_CLI='ON' \
    -DENABLE_HDR10_PLUS='OFF' \
    -DENABLE_LIBNUMA='ON' \
    -DENABLE_LIBVMAF='OFF' \
    -DENABLE_PIC='ON' \
    -DENABLE_PPA='OFF' \
    -DENABLE_SHARED='ON' \
    -DENABLE_SVT_HEVC='OFF' \
    -DENABLE_TESTS='OFF' \
    -DENABLE_VTUNE='OFF' \
    -DEXTRA_LINK_FLAGS='-L .' \
    -DHIGH_BIT_DEPTH='OFF' \
    -DMAIN10='ON' \
    -Wno-dev
  make -C build-10
    

# -DEXTRA_LIB='x265_main10.a;x265_main12.a' \

  cmake -S x265_3.5/source -B build \
    -DCMAKE_INSTALL_PREFIX='/usr' -DLIB_INSTALL_DIR='lib32' \
    -DCMAKE_LIBRARY_PATH='/usr/lib32' \
    -DDETAILED_CU_STATS='OFF' \
    -DENABLE_AGGRESSIVE_CHECKS='OFF' \
    -DENABLE_ASSEMBLY='ON' \
    -DEXPORT_C_API='ON' \
    -DENABLE_CLI='ON' \
    -DENABLE_HDR10_PLUS='ON' \
    -DENABLE_LIBNUMA='ON' \
    -DENABLE_LIBVMAF='OFF' \
    -DENABLE_PIC='ON' \
    -DENABLE_PPA='OFF' \
    -DENABLE_SHARED='ON' \
    -DENABLE_SVT_HEVC='OFF' \
    -DENABLE_TESTS='OFF' \
    -DENABLE_VTUNE='OFF' \
    -DEXTRA_LINK_FLAGS='-L.' \
    -DHIGH_BIT_DEPTH='OFF' \
    -DLINKED_10BIT='ON' \
    -DLINKED_12BIT='ON' \
    -DMAIN10='ON' \
    -Wno-dev
    ln -s ../build-10/libx265.a build/libx265_main10.a
    ln -s ../build-12/libx265.a build/libx265_main12.a
    make -C build
}

package() {
  make -C build DESTDIR="${pkgdir}" install
  rm "${pkgdir}"/usr/bin  "${pkgdir}"/usr/include -Rf
}
