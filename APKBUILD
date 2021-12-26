pkgname=wf-config-git
_repo="https://github.com/WayfireWM/wf-config"
pkgdir="${startdir}/${pkgname}"
options="!check"
pkgver="${_pkgver}_git"
pkgrel=0
provides="wf-config"
pkgdesc="Library for managing configuration files written for Wayfire"
url="https://wayfire.org"
arch="all"
license="MIT"
makedepends="
	meson
	libevdev-dev
	libxml2-dev
	glm-dev
	linux-headers
	"
options="!check" # no testsuite
subpackages="$pkgname-dev"
source=""

prepare() {
    default_prepare
    cd "${srcdir}"
    git clone "${_repo}" || return 1
    _pkgver="$(git log -1 --date=short --format="%ad" | sed 's/-/./g')"
}

build() {
    cd "${srcdir}/${pkgname}"
    abuild-meson . output
    meson compile ${JOBS:+-j ${JOBS}} -C output
}

package() {
    cd "${srcdir}/${pkgname}"
    DESTDIR="$pkgdir" meson install --no-rebuild -C output
}
