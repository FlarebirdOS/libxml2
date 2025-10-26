pkgname=libxml2
pkgver=2.15.0
pkgrel=3
pkgdesc="XML C parser and toolkit"
arch=('x86_64')
url="https://gitlab.gnome.org/GNOME/libxml2/-/wikis/home"
license=('MIT')
depends=(
    'bash'
    'glibc'
    'icu'
    'readline'
    'zlib'
    'xz'
)
makedepends=(
    'docbook-xsl'
    'doxygen'
    'meson'
    'python'
)
source=(https://download.gnome.org/sources/libxml2/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz
    https://www.w3.org/XML/Test/xmlts20130923.tar.gz)
sha256sums=(5abc766497c5b1d6d99231f662e30c99402a90d03b06c67b62d6c1179dedd561
    9b61db9f5dbffa545f4b8d78422167083a8568c59bd1129f94138f936cf6fc1f)

build() {
    cd ${pkgname}-${pkgver}

    local meson_args=(
        -D icu=enabled
        -D legacy=enabled
        -D python=enabled
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}

    ln -sv ${srcdir}/xmlconf .
}

package() {
    cd ${pkgname}-${pkgver}

    ${meson_install} ${pkgdir}

    sed '/libs=/s/xml2.*/xml2"/' -i ${pkgdir}/usr/bin/xml2-config
}
