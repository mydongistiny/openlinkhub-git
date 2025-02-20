#Maintainer: Jason Edson <jaysonedson at gmail dot com>

pkgname=openlinkhub-git
_pkgname=OpenLinkHub
pkgver=0.5.1.r3.g505a8be
pkgrel=1
pkgdesc="Open source Linux interface for iCUE LINK Hub and other Corsair AIOs, Hubs."
arch=(x86_64)
url="https://github.com/jurkovic-nikola/OpenLinkHub"
license=("GPL-3.0")
depends=(
    systemd
    systemd-libs
)
makedepends=(
    git
    go
)
provides=(openlinkhub)
conflicts=(
    openlinkhub
    openlinkhub-bin
)
install=OpenLinkHub.install
source=(
    "git+https://github.com/jurkovic-nikola/${_pkgname}"
    "OpenLinkHub.service"
    "config.json"
)
sha256sums=(
    "SKIP"
    "79001d39ab3893efe69c72869f29e20b1b85ea007e0bc5bdecc3d47bdf8975d0"
    "54703993391f8bebdf55aaeb71e918434401f3c7eb6f336bb9280262ec65a823"
)

pkgver() {
    cd ${_pkgname}
    git describe --long --tags --abbrev=7 | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd ${_pkgname}
    go build .
}

package() {
    cd ${_pkgname}

    # Copy files to /opt
    install -d "${pkgdir}/opt/${_pkgname}"
    cp -r web/ "${pkgdir}/opt/${_pkgname}"
    cp -r static/ "${pkgdir}/opt/${_pkgname}"
    cp -r database/ "${pkgdir}/opt/${_pkgname}"
    install -Dm 755 OpenLinkHub -t "${pkgdir}/opt/${_pkgname}"
    install -Dm 644 "${srcdir}/config.json" -t "${pkgdir}/opt/${_pkgname}"

    # Link binary to /usr
    install -d "${pkgdir}/usr/bin"
    ln -s /opt/${_pkgname}/${_pkgname} "${pkgdir}/usr/bin/${_pkgname}"

    # Install systemd service
    install -d "${pkgdir}/usr/lib/systemd/system/"
    install -Dm 755 "${srcdir}/OpenLinkHub.service" -t "${pkgdir}/usr/lib/systemd/system"

    # Create udev rules
    install -d "${pkgdir}/etc/udev/rules.d"
    install -Dm 644 "99-openlinkhub.rules" -t "${pkgdir}/etc/udev/rules.d"

    # Create user for service
    echo 'u openlinkhub - "OpenLinkHub interface for iCUE LINK"' |
      install -Dm644 /dev/stdin "${pkgdir}/usr/lib/sysusers.d/${pkgname%-git}.conf"
}
