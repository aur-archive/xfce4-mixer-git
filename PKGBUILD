# Maintainer: Limao Luo <luolimao+AUR@gmail.com>
#
# (Added from xfce4-mixer package)
# Contributor: Tobias Kieslich <tobias@archlinux.org>

_pkgname=xfce4-mixer
pkgname=$_pkgname-git
pkgver=4.10.0.58.ga75148a
pkgrel=1
pkgdesc="The volume control plugin for the Xfce panel"
arch=(i686 x86_64)
license=(GPL2)
url=http://git.xfce.org/apps/$_pkgname/tree/README
groups=(xfce4-git)
depends=(xfce4-panel gstreamer0.10-base libunique)
makedepends=(git xfce4-dev-tools)
optdepends=('gstreamer0.10-base-plugins:  to support basic audio hardware'
    'gstreamer0.10-good-plugins: well supported hardware'
    'gstreamer0.10-bad-plugins: not so well supported hardware'
    'gstreamer0.10-ugly-plugins: might contain questionable license hardware')
provides=($_pkgname=$pkgver)
conflicts=($_pkgname)
options=(!libtool)
install=$_pkgname.install
source=($pkgname::git://git.xfce.org/apps/$_pkgname)
sha256sums=('SKIP')
sha512sums=('SKIP')

pkgver() {
    cd $pkgname/
    git describe | sed 's/^xfce4-mixer-//;s/-/./g'
}

prepare() {
    sed -i 's:AM_CONFIG_HEADER:AC_CONFIG_HEADERS:' $pkgname/configure.ac.in
}

build() {
    cd $pkgname/
    ./autogen.sh \
        --prefix=/usr \
        --sysconfdir=/etc \
        --libexecdir=/usr/lib \
        --localstatedir=/var \
        --disable-static \
        --disable-debug
    make
}

package() {
    make -C $pkgname DESTDIR="$pkgdir" install
    sed -e 's:Name=Mixer:& Settings:g' \
        -e '/Categories=X-XFCE;/ s|Audio;Mixer;|Settings;DesktopSettings;|g' \
        -i "$pkgdir"/usr/share/applications/$_pkgname.desktop
}
