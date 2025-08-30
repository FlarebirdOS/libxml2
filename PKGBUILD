pkgname=libxml2
pkgver=2.14.5
pkgrel=1
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
makedepends=('python')
source=(https://download.gnome.org/sources/libxml2/${pkgver%.*}/${pkgname}-${pkgver}.tar.xz
    https://www.w3.org/XML/Test/xmlts20130923.tar.gz)
sha256sums=(03d006f3537616833c16c53addcdc32a0eb20e55443cba4038307e3fa7d8d44b
    9b61db9f5dbffa545f4b8d78422167083a8568c59bd1129f94138f936cf6fc1f)

build() {
    cd ${pkgname}-${pkgver}

    local configure_args=(
        --sysconfdir=/etc
        --disable-static
        --with-history
        --with-icu
        PYTHON=/usr/bin/python3
        --docdir=/usr/share/doc/${pkgname}-${pkgver}
        ${configure_options}
    )

    ./configure "${configure_args[@]}"

    make

    ln -sv ${srcdir}/xmlconf .
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install

    sed '/libs=/s/xml2.*/xml2"/' -i ${pkgdir}/usr/bin/xml2-config
}
