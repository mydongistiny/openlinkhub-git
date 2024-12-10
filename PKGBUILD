#Maintainer: Jason Edson <jaysonedson at gmail dot com>

pkgname=openlinkhub-git
_pkgname=OpenLinkHub
pkgver=0.4.0.r0.g445d4a2
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
install=OpenLinkHub.install
source=(
    "git+https://github.com/jurkovic-nikola/${_pkgname}"
    "OpenLinkHub.service"
)
sha256sums=(
    "SKIP"
    "79001d39ab3893efe69c72869f29e20b1b85ea007e0bc5bdecc3d47bdf8975d0"
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

    # Link binary to /usr
    install -d "${pkgdir}/usr/bin"
    ln -s /opt/${_pkgname}/${_pkgname} "${pkgdir}/usr/bin/${_pkgname}"

    # Install systemd service
    install -d "${pkgdir}/usr/lib/systemd/system/"
    install -Dm 755 "${srcdir}/OpenLinkHub.service" -t "${pkgdir}/usr/lib/systemd/system"

    # Create udev rules
    install -d "${pkgdir}/etc/udev/rules.d"
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-icuelink.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c3f", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-icuelink-lcd.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c4e", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-cc-64.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c32", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-lcd.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c39", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-cc-96.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c1c", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-ccxt.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c2a", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-h100i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c35", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-h100i-white.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c40", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-h115i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c36", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-h150i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c37", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-elite-h150i-white.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c41", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-lncore.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c1a", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-lnpro.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c0b", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-cpro.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c10", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-xc7-lcd.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c42", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h100i-rgb-pro-xt.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c20", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h115i-rgb-pro-xt.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c21", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h150i-rgb-pro-xt.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c22", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-xd5-lcd.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c43", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k55-core-rgb.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1bfe", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k65-pro-mini.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1bd7", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k70-core-rgb.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1bfd", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k65-plus.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="2b10", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k65-plusW.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="2b07", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-k100-air.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1bab", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-slipstream-wireless.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1bdc", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-st100.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0a34", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-mm700.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1b9b", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-lt100.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c23", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx750i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c05", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx850i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c06", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx1000i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c07", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx1000iv2.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c1e", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx1200i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c08", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx1200iv2.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c23", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-hx1500iv2.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c1f", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-rm850i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c0c", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-rm850i.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1c0d", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-katarpro.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1b93", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-ironclaw-rgb.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="1b5d", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h115i-platinum.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c17", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h100i-platinum.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c18", MODE="0666"'
    cat > "${pkgdir}/etc/udev/rules.d/99-corsair-h100i-platinum-se.rules" <<< 'KERNEL=="hidraw*", SUBSYSTEMS=="usb", ATTRS{idVendor}=="1b1c", ATTRS{idProduct}=="0c19", MODE="0666"'

    # Create user for service
    echo 'u openlinkhub - "OpenLinkHub interface for iCUE LINK"' |
      install -Dm644 /dev/stdin "${pkgdir}/usr/lib/sysusers.d/${pkgname%-git}.conf"
}
