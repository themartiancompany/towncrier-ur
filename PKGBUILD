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
pkgver=22.12.0
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
  'af602610ddf77ad2d241347bd59ac915637123b65aa9da41197674ea338f8d7c86d1faa59e58e8675286c44ea266915896041bf6e16c3e920e40ca85cf04e52d'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      build
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
    setup.py \
      install \
        -O1 \
        --root="${pkgdir}" \
        --prefix=/usr
  install \
    -Dm644 \
    LICENSE \
    -t \
      "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set sw=2 sts=-1 et:
