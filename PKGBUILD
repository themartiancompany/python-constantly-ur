# Maintainer: Felix Yan <felixonmars@archlinux.org>

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
_proj="twisted"
_pkg=constantly
_pkgname="${_pkg}"
pkgname="${_py}-${_pkg}"
pkgver=23.10.4
pkgrel=14
pkgdesc='Symbolic constants in Python'
arch=(
  'any'
)
license=(
  'MIT'
)
_http="https://github.com"
_ns="${_proj}"
url="${_http}/${_ns}/${_pkg}"
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
  "${_py}-versioneer"
)
checkdepends=(
  'python-pytest'
  'python-twisted'
)
source=(
  "${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha512sums=(
  'eeaa74552fe8e01c40566ac3c8b3d41085f800863ac516e30fe1242f40d3401e4e872279149776f29d3ba78a7a16337a794ad26230efab4dd1847d42bffa81ce'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    -nw
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  pytest
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim:set ts=2 sw=2 et:
