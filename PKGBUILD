# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=towncrier
pkgname="${_py}-${_pkg}"
pkgver=24.8.0
pkgrel=3
_pkgdesc=(
  "Utility to produce useful,"
  "summarised news files for your project"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com" 
_ns="hawkowl"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-click"
  "${_py}-click-default-group"
  "${_py}-incremental"
  "${_py}-jinja"
  "${_py}-setuptools"
  "${_py}-tomli"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
)
checkdepends=(
  'git'
  "${_py}-twisted"
)
provides=(
  "${_pkg}=${pkgver}"
)
_pypi="https://pypi.io/packages/source"
source=(
  "${_pypi}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  'b01998230936e920a5ad0b4c18f73686ea557fc47f6346fed4c7b3aabec6bceb5b822fa951cd7dec4e1dcd3d6f8e9a6cccebb1aa6ca3f7f56557c8d31c3be5bd'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation

#   "${_py}" \
#     setup.py \
#       build
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="$PWD/tmp_install" \
        --optimize=1
  PYTHONPATH="${PWD}/tmp_install/usr/lib/python${_pymajver}/site-packages" \
  PATH="$PWD/tmp_install/usr/bin:$PATH" \
  trial \
    towncrier
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # "${_py}" \
  #   setup.py \
  #     install \
  #       -O1 \
  #       --root="${pkgdir}" \
  #       --prefix=/usr
  install \
    -Dm644 \
    LICENSE \
    -t \
      "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set sw=2 sts=-1 et:
